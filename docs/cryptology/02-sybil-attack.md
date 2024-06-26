---
slug: /sybil-attack
---

# 2. 女巫攻击

# 什么是女巫攻击
之前的文章在讲拜赞庭容错的时候，我们提到了女巫攻击Sybil Attack。那什么是女巫攻击呢？ 

女巫攻击这个词来源于Flora Rheta Schreiber 在1973年的小说《女巫》，这本小说写的是对兼具多种人格的Sybil Dorsett进行心理治疗的故事。一人化身为多人，这个就是女巫攻击的本质。

在一个单纯的分布式P2P网络中，任何节点可以随意的加入和退出P2P网络，没有任何限制。它只需要对外暴露其在P2P网络中的唯一标志即可，除此之外，其他的信息都是私有的。

鉴于P2P网络分布式的特性，这就意味着没有任何中心节点，或者说没有特权节点。这样即使大家发现了恶意的节点，也没有权利去回滚整个网络的操作。在P2P网络中，我们必须假设所有的节点都是不可靠的，跟所有其他节点的交互都是有风险的。

女巫攻击正是利用了P2P网络的分布式特性，将一个节点伪装成多个节点，并将这多个伪装节点（也叫做Sybil 节点）广播到整个P2P网络中，从而做一些莫可名状的事情，比如获得网络控制权，拒绝响应，干扰查询等事情。

考虑到之前我们提到的拜赞庭容错，如果发生了女巫攻击，一个节点可以伪装成多个有效节点，这样只要伪装的节点突破n/3的限制，就能控制整个网络。而实际上，恶意节点可能只有一个。

# 女巫攻击的防范
事实上，在某些P2P网络中，女巫攻击并不需要花费太多功夫即可完成。那么我们我们怎么去防范女巫攻击呢？ 

## 身份验证
既然女巫攻击的方法就是伪造网络ID，那么最简单的办法就是让每个加入的节点来做身份认证。这样伪造的节点无法通过认证，那么女巫攻击就完美的解决了。

身份验证也有两种方式：

1. 通过统一的第三方机构对节点进行认证。熟悉区块链的同学可能有听过‘oracles’，这个就是一个第三方的可信机构。当然这样做，会损失认证节点的一部分匿名性。如果参与的P2P节点可以接受，那么这确实是一个可行的办法。

2014年上映了一部德国的片子《我是谁：没有绝对安全的系统》，这个片子是讲的黑客的故事，同样的，这个世界上也没有绝对匿名的系统。世界上比较有名的像比特币,洋葱路由等都可以通过某些办法获得用户信息，这些我会在后面的文章中具体讲述。

2. 还有一种就是非直接认证。
可以假如网络初始有N的可信任节点，这些信任节点可以对其他节点进行担保，担保其他的节点也是可信任的。当然这里面涉及到一些有效的担保算法，这里就不详细讲述了。

## 特征向量
我们在做大数据的时候，往往需要通过很多特征向量来区分出是不是同一个用户，同样的在P2P网络中，我们也可以通过这种特征向量来区分这个节点是不是伪造的节点。当然这种方式不能完全避免女巫攻击，但是可以有效的减少女巫攻击。这种是有成熟产品的，像SybilGuard 和 the Advogato Trust Metric。

## 让伪造变得困难
如果能够加大伪造的难度，那么女巫攻击也就不那么有效了。这种最常见的就是POW了，工作量证明，让节点通过运算去解决问题，解决了才认可你是一个有效的节点，这样就有效的杜绝了女巫节点的存在。

## Model 0
在golem网络中，他们发明了一种算法来杜绝女巫攻击，叫做Model 0。 golem是一个算力付费的区块链项目，用户付费然后在区块链网络上面完成计算。

在Model 0中，有两种节点：Known 和 unknown， 并且会保存所有请求者的请求历史。如果一个请求者他历史记录里面有3-5个成功交易，那么这个请求者就是Known节点，其他的没有发生过交易的就是unknown节点。

系统如果一直和Known节点进行交互当然不会出现任何问题，但是Known节点毕竟是有限的，那么系统还是要接收一定的Unknown节点。怎么保证接收Unknown节点的过程中，不会受到女巫攻击呢？ 

办法就是构造一个量化的机制，当节点跟Unknown节点进行交互的过程中，如果出现错误或者失败，那么节点可以暂时拒绝和Unknown节点的请求，只接收Known节点的请求。在未来的某个时间再去接收Unknown节点的请求，这样就保证了系统在整体上是可用的，不会出现大面积服务拒绝的情况。



更多教程请参考 [flydean的博客](http://www.flydean.com/sybil-attack/)




