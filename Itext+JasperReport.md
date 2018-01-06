## itext

[官方网站](https://itextpdf.com)

### 概述

在企业的信息系统中，报表处理一直占比较重要的作用，iText是一种生成PDF报表的Java组件。通过在服务器端使用Jsp或JavaBean生成PDF报表，客户端采用超链接显示或下载得到生成的报表，这样就很好的解决了B/S系统的报表处理问题。

maven坐标

```
<dependency>
    <groupId>com.lowagie</groupId>
    <artifactId>itext</artifactId>
    <version>2.1.7</version>
</dependency>
<dependency>
    <groupId>com.itextpdf</groupId>
    <artifactId>itext-asian</artifactId>
    <version>5.2.0</version>
</dependency>
```

## JasperReport

### 概述

对Itext进行封装,相当于hibernate与jdbc的关系,使编码更容易

maven坐标

```
<!-- jasperreport -->
<dependency>
    <groupId>net.sf.jasperreports</groupId>
    <artifactId>jasperreports</artifactId>
    <version>5.2.0</version>
    <exclusions>
        <exclusion>
            <groupId>com.lowagie</groupId>
            <artifactId>itext</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

## IReport

###概述

iReport 是为JasperReports Library和JasperReports Server设计的报表可视化设计器。
iReport的遵循AGPL自由开源协议，在SourceForge.net开源社区发布[1]  。
根据iReport和Jasper Studio的维护公告，自iReport版本5.5.0之后，终止新功能的开发。在2015年12月31日以前，对iReport的维护仅限于严重缺陷的修复，不会再增加新的功能。