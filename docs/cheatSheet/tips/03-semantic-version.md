---
slug: /03-semantic-version
---

# 5. 小知识系列:让版本出来说话
# 简介

不知道大家都是怎么定义软件的版本号的？是老老实实的从1.0版本开始，还是像埃里森那样直接从2.0开始，还是从beta版本0.x开始呢？

虽然一眼看过去，我们肯定会希望使用版本号最高的那款软件，因为版本号越高，代表着其迭代越多，功能越稳定。

这里不讨论版本高低的好坏，这里要讨论的是如何让版本说话。

# 让版本说话

为什么要让版本说话？版本会怎么说话呢？

让版本说话的意思是，版本本身就代表一定的含义，通过版本号就可以基本了解这个版本的大致情况。

# 为什么需要管控版本

那么为什么要管控版本呢？那是因为在现代的应用中，一个项目需要大量依赖第三方项目，而第三方项目又会依赖其他的项目，从而生成一个庞大的依赖集合。

在这种庞大的版本依赖情况下，我们需要大致上知道现有的项目可以依赖第三方项目的大致版本范围，从而在依赖项目版本升级的情况下，不至于导致本项目出现问题。

所以我们需要一个版本制定规则。

这就是我们今天要讲的语义化版本.

# 语义化版本规范

在语义化版本中，版本号是由三部分组成的,它的格式是：X.Y.Z（主版本号.次版本号.修订号）。

如果只是bug的修复，而不影响 API 时，递增修订号,如果API 保持向下兼容的新增及修改时，递增次版本号；如果进行不向下兼容的修改时，递增主版本号。

这样要用什么样的版本是不是很清晰了？

具体而言，X、Y 和 Z 为非负的整数，其中X 是主版本号、Y 是次版本号、而 Z 为修订号。并且需要遵循下面的一些原则，以保证语义化版本规范的正确性。 我们看下有哪些规则：

1. 在一个版本发布后，禁止对改版本再进行修改。如果需要修改，则递增版本号。

2. 主版本号为0的版本，如0.1.3,表示软件还在初始的开发阶段，软件并不稳定。

3. 1.0.0 之后的版本才被视为稳定的版本。

4. 如果是对API进行内部的bug修复，则递增Z的值。

5. 如果是新增了向下兼容的新功能，则递增Y的值。如果有API被标记为废弃的话，也需要递增Y的值。也可以在包含大量的新功能的时候递增Y值。每当Y值递增的时候，Z值需要归零。

6. Y会在添加任何不向下兼容的API的时候进行递增。每当主版本号递增时，次版本号和修订号必须归零.

7. 除了主版本之外，还可以在主版本后面添加上先行版本号. 先行版本号是由数字和字母组合而成，以一个连接号接在主版本后面。比如1.0.0-alpha、1.0.0-alpha.1、1.0.0-0.3.7、1.0.0-x.7.z.92。先行版本号表示这个版本并非稳定而且可能无法满足预期的兼容性需求。

8. 在先行版本号或者主版本号后面还可以加上编译版本号。编译版本号也是由数字和字母组合而成，以一个加号接在主版本或者先行版本号的后面。如：1.0.0-alpha+001、1.0.0+20130313144700、1.0.0-beta+exp.sha.5114f85。

# 总结

以上就是语义化版本的基本说明，如果大家都按照上面提到的语义化规范来进行版本的编写话，那么我们的软件世界将会变得无限美好。





