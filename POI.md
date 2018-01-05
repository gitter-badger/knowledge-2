##excel读写工具-POI
###介绍

目前常见读写Excel的工具类开源JavaAPI有两种方式

1. JXL(Java Execl API) [官方网站](http://jexcelapi.sourceforge.net/)
2. Apache的POI(Poor Obfuscation Implementation) [官方网站](http://poi.apache.org)

* POI支持微软的OLE2格式文件Office2003及以下版本,同时支持微软OOXML(Office Open XML)标准,也就是Office2007以上版本.JXL只能实现对Excel2003以下版本的支持.

* POI使用HFFS对象操作OLE2格式Excel,文件后缀为.xls的;使用XSSF,SXSSF对象操作OOXML格式Excel,文件后缀为.xlsx的.

* 对于OLE2版本的Excel,一个Sheet工作表它的行最多支持到65536行,列支持到256列;

* 对于OOXML版本的Excel,一个Sheet工作表它的行最多支持到1048576行,列支持到65536列.

###核心API



###POI读写大数据量EXCEL

有三种模式:
1. eventmodel方式,基于事件驱动,SAX的方式解析Excel(.xlsx是基于OOXML的),CPU和内存消耗非常低,但是只能读不能写
2. usermodel,就是我们一般使用的方式,这种方式可以读写,但是CPU和内存消耗非常大
3. SXSSF,POI3.8以后开始支持,这种方式只能写Excel

采用的读取方式是事件模型eventusermodel,因为excel2007采用的存储方式实际上是xml形式