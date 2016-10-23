# 记一个同时支持模糊匹配和静态推导的Atom语法补全插件的开发过程: 序

![模糊提示](https://github.com/ios122/apicloud_autocomplete_atom_readme/blob/master/0_0.png?raw=true)

![静态推导](https://github.com/ios122/apicloud_autocomplete_atom_readme/blob/master/0_1.png?raw=true)

## 简介

过去的一周,都睡的很晚,终于做出了Atom上的APICloud语法提示与补全插件:[apicloud_autocomplete ](https://github.com/apicloudcom/apicloud_autocomplete_atom).个中滋味,感觉还是有必要记录下来的.代码基于 *GPL-3.0* 开源,所以我可以较为详细的记录一些很难被理解和体会的技术细节.APICloud目前已有Studio,VSCode,Webstrom和Sublime的语法补全插件,但是毫无疑问,我做的这款,是目前为止最好的 -- 唯一的一个支持100%所有API,唯一的一个同时支持模糊匹配和静态推导语法提示插件!

可能你会说,估计是Atom语法补全的扩展机制灵活等等吧!但是,我可以很明确地告诉你,核心逻辑是基于正则匹配的通用逻辑,和Atom没有必然的联系! *apicloud_autocomplete* ,需要多个技术栈的创造性地混合使用,某种程度上,这个系列的文章,就是写给全栈开发工程师的赞歌!哈哈~

## 你会耐心读完整个系列文章的N个可能性

* 你可能想做一个ReactNative或者Weex的API级别的语法提示与补全插件!注意,我说的是精确到特定API的提示,而不是简单的通用语法提示.比如现在有好多jsx语法自动补全的提示,但是并没有能真正提示某个模块的某个方法或者某个属性的ReactNative或者Weex的插件.
* 你可能对网页数据的针对性抽取感兴趣.从HTML格式的数据中,按照特定规则,抽离特定的数据,正则固然可以,但是我推荐你使用 [pup](https://github.com/ericchiang/pup).这个Task,使用了非常复杂的pup使用技巧,值得一读.
* 你可能对正则表达式的深入使用感兴趣.刚开始,基于Atom的分析树写的,但是通用性太弱,后来就改成基于正则的了.展示了一些复杂的正则用法,比如后向匹配.不得不说,正则表达式式,太强大了!
* 你可能对较大量数据的清洗和格式化感兴趣.文章将展示一些你可能以后也会需要的shell脚本.顺序很重要!

## 难点与技术点一览

* 海量数据,却没有现成的获取模块api信息的通用接口.300多个模块,几千条api,如果一条条录入其方法名,代码模块,没有 **30** 天,真的很难搞定!但是,我只用了 **3** 天!简单的shell知识,还是挺有帮助的.
* 模糊提示.这个是很实用的功能,实现起来还是需要一点点正则技巧的.
* 静态推导,即根据上下文推断变量正式模块类型.仔细想想,或许你能理解问题的困难之处 -- 你只是一个语法提示,是不能真实地执行代码的,你要做一个静态分析,来推断出某个变量对应的模块的类型,进而在其模块信息内部搜索相关的api提示!

## 系列文章规划

现在的工作,我很难每天都有时间去写博客.尽量这个系列在周内更新完;如果delay了,还请见谅!当然,插件本身的逻辑代码已经写就,大家可以直接去看github上阅读:[apicloud_autocomplete 插件源码](https://github.com/apicloudcom/apicloud_autocomplete_atom)

* (一) 抓取需要的模块信息. -- 会分享一个基于公开文档的完整的模块信息数据压缩包呦!

* (二) apicloud_autocomplete 架构设计与实现.  -- 会着重讲述"模糊匹配"与"静态推导"的正则技巧.

* (三) 清洗数据,导入插件.  --你在看的时候,更多有价值的信息在数据清洗部分;但是我想说的是,当你把完整的真实数据导入既定功能代码中,当插件终于有了完整数据,被赋予完整生命,竟然还能运行的时候,那种兴奋,真的是很难言表!大家有兴趣,有时间,一定要自己搞下这个!

## 关于 GPL-3.0

我努力寻找商业竞争和技术共享之间的结合点,目前为止我发现基于 *GPL-3.0* 可以很好地平衡这两点.

* 他人修改代码后,不可以闭源;
* 新增代码,不需要采用同样许可证;
* 不需要对源码的修改之处,提供说明文档;

## 参考资源

* [apicloud_autocomplete 插件源码](https://github.com/apicloudcom/apicloud_autocomplete_atom)
* [apicloud_autocomplete 源码分析](https://github.com/ios122/apicloud_autocomplete_atom_readme)
* [Parsing HTML at the command line](https://github.com/ericchiang/pup)
* [View and insert possible completions in the editor while typing](https://github.com/atom/autocomplete-plus)
* [主流开源协议的异同比较？](https://www.zhihu.com/question/19568896)
