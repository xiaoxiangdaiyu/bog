---
title: YAMLvsJSONvsXML 
date: 2020-07-03
---
 # YAML & JSON &XML 孰强孰弱
## 前言  
本文翻译[https://www.csestack.org/yaml-vs-json-vs-xml-difference/](https://www.csestack.org/yaml-vs-json-vs-xml-difference/),下文会针对当前现有的数据序列化语言做下梳理。重点突出YAML是什么，优缺点，和YML/JSON对比，以便于大家依据自己场景选择合适的语言。
<!-- more -->

## YAMML 简介
YAML和JSON、XML一样是数据序列化语言，使用缩进来描述格式化数据。
下面的例子可以看到其如何工作的： 
<img src="https://p0.meituan.net/dprainbow/538a4132067ca049bdaadbce9776fc9b68328.jpg">

就像Python一样有个缩进约束，假如有过python开发体验的话，就会很明显的发现其使用缩进的数量来定义不同的区块。正如前面提到，有很多如JSON、XML这样被广泛使用的序列化语言。
### YAML使用场景
对于序列化语言来说，使用场景如下：
* 与服务器之间传输数据
* 使用一个配置文件来配置应用，这些文件声明对应参数和相应取值
* 在同一个应用不同组件之间转换数据
* 中间数据存储
针对此类场景，YAML有一些明确的优势相比于其他同类语言。也是为什么现在越来越多的开发者使用其的地方。
### YAML的优势
* YAML中没有额外的定界符，所以相比JSON或者XML更轻量级。
* 没有额外定界符，所以更易读(这里持原作者和译者都持保留观点，不少开发者认为有定界符的可读性更强。)
* YAML使数据更易于理解，因此常用于配置文件中(观点同上)
* 应用比价哦广泛，除配置文件之外，传输数据和中间存储都有实践。
* YAML是JSON 的超集，对于合法的JSON代码，同样可以被YAML解析，这样对于使用JSON和YAML的应用来说，可以使用一个解析器完成两种解析。
然而其并没有如期望中那样受欢迎，具体而言，因为不同的序列化语言都有其特定的适宜语言或者场景（下文可以提到），并且YAML有一些不足相较于其他广泛使用的序列化语言。

### YAML的不足
* 相对年轻，早期很多应用已经使用JONS或者XML来构建，对于开发者来说迁移至YAML成本是十分高的。
  举例，假如我们负责的项目是使用XML的，就算我们开发独立的插件也会倾向于XML以便更加契合。
* 流行广泛程度反向作用域生态系统，例如XML 有着比YAML极为成熟的生态。JSON从2000年开始出现，同样被高度采用。因此在YAML上可以找到对JSON的支持(译者注：既有向现实妥协的味道，也是聪明的做法)
* YAML中有很多方式来体系化数据层级，因此处理时会相对复杂些。性能上相对于XML和JSON会有差别。
* 可能一些开发人员发现很难使用其复杂的缩进格式。

## 三种概述
YAML，XML和JSON是常用的数据序列化语言，下面会针对三者之间的不同展开叙述。原作者针对如何选择适合自己项目的数据序列化语言给出了部分建议，以供参考。  
## 三者直观对比
* YAM 是 'YAML Aint Markup Language'(YAML不是一种标记语言😄)的缩写，本意在强调其以数据作为重心，而非标记语言。
* JSON 比较直白 “JavaScript Object Notation“( JS 对象标记)，一种轻量级的数据交换格式，与js天然契合。
* XML 是 “eXtensible Markup Language”(可扩展标记语言)，这里再看YML，其强调自己不是标记语言。
* XML和HTML相同，使用标签来定义数据结构
* YAML使用缩进来定义结构化数据，因此每个YAML中的数据块通过空白的数量来区分
* 三者文件的扩展名都与其名称对应， .yaml for YAML, .json for JSON, .xml for XML，比较容易记忆。
* 实际上，三者的扩展名都是比较随意的，对开发者和应用来说重要的是其文件格式，内容类型和数据结构。(译者按，重要的是内容，例如.yml和.yaml几乎无差别。.js的文件中依然可以存储json).

## 示例
### yaml
YAML的例子中，比较个性的就是每个数据块都有相对应的空白格。
这里就直接照搬原文示例了： 
<img src="https://p0.meituan.net/dprainbow/538a4132067ca049bdaadbce9776fc9b68328.jpg">

### json
<img src="https://p0.meituan.net/dprainbow/a8ad2577e5fe559a77a11e59af0a37cc85837.jpg"/>

### xml
<img src="https://p0.meituan.net/dprainbow/4a1f2b10703f364f481d5cf6911bd9df119899.jpg"/>

## 三者在应用中的不同表现
现在时候，大家发现三者的不同取决于在何种应用中使用。
* 当提到javascript的时候，JSON是最适合的序列化语言
* 对于java开发者来说，张嘴闭嘴就是xml
* Python和YAML有相同的空格赎金，所以对于Pythoner们来说，YAML是更友好的选择
从上面可以看出，使用哪一种序列化语言，取决于你在使用什么技术栈。

### 如何选择序列化语言
数据以良好的数据结构存储在不同序列化语言中，无论使用哪一种，都要包含以下四种主要的活动：
* 将内容从序列化语言中解析
* 读取所需的值
* 操作对应值
* 很可能，还得将操作之后的值塞回到序列化语言中去
要实现以上几种开发行为，你必须要可以解析的代码，幸运的是，市面上已经有很多开源支持常见语言(像c,c++,java等)的工具包或者库来解析序列化之后的数据。
### 为什么不应该花费时间来开发解析器
首先自己开发可能存在一些问题，使用优秀的开源包来避免该问题，当然还节约时间。
因此在使用某一种序列化语言之前，首先应该查找解析器，阅读文档， 选择合适自己项目的序列化语言。对于自己来说，简单的调用方法就能解决的事情当然要比自己手动实现要好。
### 反其道而行之
虽然都说Python与YMAL更搭，但是原作者在Python项目中却选择了JSON。对此其理由如下：
原作者负责的是符合Redfish标准的，使用REST API和bottle 框架（一个Python框架），核心语言是Python的一个项目。同样面临着需要在服务器和客户端转换数据的场景，选中JSON作为序列化语言，业界早已存在Python语言开发的转义包。导致这个选择的重要原因是，Python的字典和所以的序列化语言一样不过是使用name-value存储数据的代码，仔细查看会发现JSON 的map是格式更接近Python的字典。


## 结束语
到这里，三种序列化语言异同的介绍就结束了，希望能有所帮助。对于数据序列化语言来说，每一种都是关于数据表示格式，但从功能来说，并没有优劣之分，每一种都有其适合的场景。更重要的是，开发人员对理解和解析序列化语言的舒适度才是重要的。[更多文章请移步我的博客](https://github.com/xiaoxiangdaiyu/blog)
### 感谢
再次感谢原作者的两篇文章
* [Advantages and Disadvantages of YAML over XML and JSON](https://www.csestack.org/advantages-disadvantages-yaml/) 
* [YAML vs JSON vs XML | What is the Difference Between Them?](https://www.csestack.org/yaml-vs-json-vs-xml-difference/)  
#### 参考文章 
* [官方文档](https://yaml.org/spec/1.2/spec.html) 