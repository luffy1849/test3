HTTP系列之:HTTP缓存

[toc]

# 简介

为了提高网站的访问速度和效率，我们需要设计各种各样的缓存，通过缓存可以避免不必要的额外数据传输和请求，从而提升网站的请求速度。对于HTTP协议来说，本身就自带有HTTP缓存。

今天我们就深入探讨一下HTTP中的缓存机制和使用。

# HTTP中的缓存种类

缓存就是将请求的资源在本地保存一份拷贝，从而在下一次请求的时候，直接返回该拷贝，不用再从服务器下载资源，从而减少了资源的传输提升了效率。

除了直接访问和返回资源之外，HTTP中的缓存可以分成两类，一种是共享cache，也就是说不同的客户端都可以从该共享cache中获取资源，并且这些资源是多个客户端可以访问的。还有一种是私有cache，这意味着该cache只能用户或者客户端私有访问，其他用户是无权访问的。

私有cache很好理解，我们常用的浏览器中的cache基本上就是私有cache，这些cache是浏览器独有的，并不会共享给其他的浏览器。

共享cache主要用在一些web代理上，比如web代理服务器，因为web代理服务器可能会为众多的用户提供资源服务，对于这些用户共同访问的资源就不必要每个用户保存一份了，只需要在web代理服务器中保存一份即可，这样可以减少资源的无效拷贝。

# HTTP中缓存响应的状态

对于HTTP缓存来说，一般缓存的是GET请求，因为GET请求除了URI之外，并没有其他多余的参数，并且其表示的意义是从服务器获取资源。

不同的GET请求，会返回不同的状态码。

如果是成功返回资源，则会返回200表示OK。

如果是重定向，则返回301。如果是异常，则返回404。如果是不完全的结果，则会返回206。

# HTTP中的缓存控制

HTTP中的缓存控制是通过HTTP头来表示的。在HTTP1.1中加入了Cache-Control，我们可以通过Cache-Control来控制请求和响应的缓存情况。

如果不需要缓存，则使用：

```
Cache-Control: no-store
```

如果需要对客户端的缓存进行验证，则使用：

```
Cache-Control: no-cache
```

如果要强制进行验证，则可以使用：

```
Cache-Control: must-revalidate
```

在这种情况下，过期的资源将不会被允许使用。

对于服务器来说，可以通过Cache-Control来控制缓存是private或者public的：

```
Cache-Control: private
Cache-Control: public
```

还有一个非常重要的缓存控制就是过期时间：

```
Cache-Control: max-age=31536000
```
通过设置max-age，可以覆盖Expires头，表示在这个时间区间范围之类，该资源可以看做是最新的，不需要重新从服务器获取。

Cache-Control是HTTP1.1中定义的header字段，在HTTP1.0中也有一个类似的字段叫做Pragma。通过设置 Pragma: no-cache可以得到类似Cache-Control: no-cache的效果。也就是强制客户端重新提交缓存到服务器端进行校验。

但是对于服务器端的响应来说，并不包含Pragma，所以Pragma并不能完全替代Cache-Control。

# 缓存刷新

缓存存放在客户端之后，就可以在请求的时候被使用了。但是为了安全起见，我们需要给缓存设置一个过期时间，只有在过期时间之前的时间范围，缓存才是有效的，如果超过了过期时间，则需要从服务器重新获取。

这样的机制能够保证客户端获取到的资源始终是最新的。并且能够保证服务器端对资源的更新能够及时到达客户端。

如果客户端的资源在过期时间之类，那么这个资源的状态就是fresh，否则资源的状态就是stale。

如果资源是stale状态的，该资源并不会立即从客户端清理出去，而是在下一次的请求中，向服务器发送一个If-None-Match的请求，判断该资源在服务器端是否仍然是fresh状态的，如果该资源并没有发生变化，则返回304 (Not Modified)，表示该资源仍然有效。

而这个fresh的持续时间就是通过"Cache-Control: max-age=N" 来判断的。

如果响应中并没有这个头，则会去判断 Expires header 是否存在，如果存在那么fresh的时间就可以使用Expires - Date 来进行计算。

如果响应中连Expires header都没有，那么怎么去判断资源的fresh时间呢？

这种情况下会去查找Last-Modified header，如果这个header存在的话，那么fresh时间就是（Date - Last-modified ）/ 10 。

## revving

为了提升HTTP请求的效率，我们当然希望缓存时间越长越好，但是前面我们也提到了，缓存时间过长会导致服务器资源更新困难的问题。怎么解决呢？

对于那些不经常更新的文件，请求他们的URL可以由文件名+版本号来决定。同一个版本号表示该资源内容是固定不变的，我们可以对其缓存一个非常长的时间。

当服务器资源内容发生变化之后，只需要在请求的时候更新版本号即可。

虽然这样的操作会造成服务器资源的修改同时要修改客户端请求的版本，但是在现代前端打包工具的帮助下，这并不是一个很大的问题。

# 缓存校验

当缓存的资源过期之后，有两种处理方式，一种是重新从服务器请求资源，一种是对缓存资源进行再次校验。

当然再次校验需要服务器的支持，并需要设置"Cache-Control: must-revalidate"请求头。

那么客户端怎么去校验资源是否有效呢？很明显我们不能把资源从客户端发送到服务器端进行校验，这样的操作方式太过复杂，并且在文件比较大的请求下，会造成资源的浪费。

我们很容易想到的一种方法是对资源文件进行hash运行，只要发送这个hash运算的结果进行对比即可。

当然，在HTTP中，提供了一个ETags header，这header可以看做是资源的唯一标记，用来在客户端和服务器端进行校验。这样客户端就可以请求一个If-None-Match，让服务器判断该资源是否match。这种判断被称为强校验。

还有一种弱校验的方式，如果响应中带有Last-Modified，则客户端可以请求一个If-Modified-Since，来向服务器询问该文件是否发生了变化。

对于服务器端来说，它可以选择是否进行文件的校验，如果不进行校验，则可以直接返回一个200 OK状态码，并直接返回资源。如果进行校验，则返回一个304 Not Modified，表示客户端可以继续使用缓存的资源，同时还可返回一些其他的header字段，比如更新缓存的过期时间等。

# Vary响应

在服务器响应的时候，可以带上Vary header。这个Vary header的值是响应头中的某个key，比如Content-Encoding，表示对某个encoding的资源进行缓存。

比如客户端首先请求：

```
GET /resource HTTP/1.1
Accept-Encoding: * 
```

服务器端返回：

```
HTTP/1.1 200 OK
Content-Encoding: gzip
Vary: Content-Encoding
```

则将会把资源和gzip类型的Content-Encoding一起缓存起来。

当客户再次请求：
```
GET /resource HTTP/1.1
Accept-Encoding: br
```

因为当前缓存的资源encoding方式是gzip，和客户端接受的encoding方式并不一样，所以重新需要从服务器获取：

```
HTTP/1.1 200 OK
Content-Encoding: br
Vary: Content-Encoding
```

这时候，客户端又缓存了一个br格式的资源。

下次客户端再次请求br类型的资源，就可以命中缓存了。

总结一下，Vary的意思是将资源再通过其他的类型比如encoding进行区分和缓存。

但是这样也会造成资源重复存储的问题，同一个资源因为编码格式的不同被缓存了很多份。为了解决这个问题，就需要对资源请求进行标准化。

所谓标准化，就是在请求之前对请求的encoding方式进行校验，只选择其中的一种编码方式进行请求，从而避免资源多次缓存的情况。

# 总结

到此，HTTP缓存就介绍完毕了，大家可以在实际的应用中对HTTP缓存加深理解。







