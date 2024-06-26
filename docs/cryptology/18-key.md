---
slug: /key
---

# 18. 密钥详解

在之前的文章中，我们讲到了对称密码，公钥密码，消息认证码和数字签名等密码学的技术，这些技术中都使用到了一个叫做密钥的东西。

那么到底什么是密钥呢？密钥就是一个key，通过这个key可以获得最终的明文。所以密钥其实是和明文等价的。

举个例子，保险箱里面放着十万美元，保险箱被锁住了，并且有一个钥匙。那么这个拥有钥匙的人和拥有了十万美元是等价的。

## 各种密钥总结

之前的文章中，我们分别讲到了对称密码，公钥密码，消息认证码和数字签名这四种密码学技术。这里我们再来回顾一下。

* 对称密码

![](https://img-blog.csdnimg.cn/20200331134452961.png)

对称密码使用相同的密钥来进行明文的加密和解密。

* 公钥密码

![](https://img-blog.csdnimg.cn/20200331134503633.png)

公钥密码使用不同的密钥来对消息进行加密解密。

* 消息认证码

![](https://img-blog.csdnimg.cn/20200331134515488.png)

消息认证码使用相同的密钥来对消息进行认证。

* 数字签名

![](https://img-blog.csdnimg.cn/20200331134524955.png)

数字签名使用不同的密钥来对消息进行签名和验证。

其中对称密码和公钥密码是直接对明文进行加密，从而用来保证消息的机密性。

而消息认证码和数字签名则是用来做消息的认证，其本身并不用作对明文的加密，主要来验证消息的合法性。

## 其他密钥分类

上面的四种是按照加密方式和使用用途来分的，其实安装密钥的使用次数可以分为会话密钥和主密钥。

会话密钥是只用在一个会话中的密钥，用完之后就废弃不用了，而主密钥是固定的密钥，一直重复使用的密钥。

熟悉SSL/TLS协议的朋友肯定对这个比较熟悉，在这个协议中每次会话都会创建一个单独的密钥用来加密会话消息，也就是说每次会话都会创建一个会话密钥。

另外安装加密对象是内容还是密钥，我们可以分为加密消息的密钥（CEK）和加密密钥的密钥（KEK）。加密消息的密钥很好理解，之前的对称密钥和公钥密钥就是CEK。而加密密钥的密钥主要是为了减少密钥的保存个数。

## 密钥的管理

我们主要从下面几个方面来讲解密钥的管理：

1. 生成密钥

生成密钥有两种方式，使用随机数和使用口令。

随机数一定要有不可被推断的特性，一般来说我们需要使用伪随机送生成器来生成。

java代码中我们通常会用到Random类，但是这个类是不能用来生成密钥的。我们可以使用java.security.SecureRandom来生成密码安全的随机数。

下面是SecureRandom的两种常用用法：

~~~java
        SecureRandom random = new SecureRandom();
        byte bytes[] = new byte[20];
        random.nextBytes(bytes);
~~~

~~~java
 byte seed[] = random.generateSeed(20);
~~~

除了随机数，另外一种方式就是口令了。

口令是人类可以记住的密码，为了保证口令生成的密钥不会被暴力破解，需要对口令加盐。 

简单点说就是向口令添加一个随机数，然后对添加之后的数进行hash计算，计算出来的结果就可以当做密钥了。

2. 配送密钥

为了配送密钥我们可以采用事先共享密钥，使用密钥分配中心，使用公钥密码等方式。当然还可以采用其他的方式来配送。

3. 更新密钥

有的时候，为了保证密钥的安全，我们需要不定期的更新密钥，一般的做法就是使用当前的密钥作为一个基准值，通过特定的算法计算出新的密钥。

4. 保存密钥

学过区块链的应该都知道有个纸密钥的东西，实际上就是把密钥写在纸上进行保存。

当密钥太多的话，离线保存密钥也成了一个非常困难的工作。这时候就可以使用到密钥的密钥KEK。将这些密钥加密后保存。

这样加密后的密钥我们不用特别考虑其安全性，因为即使被窃取也无法还原之前的密钥。我们只需要保存加密这些密钥的密钥即可。

5. 作废密钥

作废密钥是个非常比较复杂的事情，因为密钥就是密钥，即使你把它删除，其他的人也可能持有它的备份。所以在设计的时候要充分考虑到密钥作废的情况。

之前的证书一文中，我们可以通过CRL列表来保存废弃的密钥。

更多内容请访问 [flydean的博客](http://www.flydean.com)
