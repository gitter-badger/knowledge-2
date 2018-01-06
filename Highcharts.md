## 报表工具 Highcharts

[官方网站](http://www.hcharts.cn)

### Highcharts是什么

Highcharts是一个用纯JavaScript编写的一个图表库,能够很简单便捷的在Web网站或者Web应用程序添加有交互性的图表,并且免费提供给个人学习,个人网站和非商业用途使用.

Highcharts支持的图表类型有直线图,区域图,柱状图,饼状图,散状点图,仪表图,气泡图,瀑布流图等多达20多种图表,其中很多图表可以集成在同一个图形中形成混合图.

### Highcharts特性

* 兼容性 - 支持所有主流浏览器和移动平台(Android,iOS等)
* 多设备 - 支持多种设备,如手持设备 iPhone/iPad,平板等
* 免费使用 - 开源免费
* 轻量 - Highcharts内核大小只有35kB左右
* 配置简单 - 使用json格式配置
* 动态 - 可以在图标生成后修改
* 多维 - 支持多维图表
* 配置提示工具 - 鼠标移动到图表的某一点上有提示信息
* 时间轴 - 可以精确到毫秒
* 导出 - 表格可以导出为PDF/PNG/JPG/SVG格式
* 可变焦 - 选中图表部分放大,近距离观察图表
* 外部数据 - 从服务器载入动态数据
* 文字旋转 - 支持在任意方向的标签旋转

### 在哪里使用Highcharts?

考虑有这种情况,当正在开发一个应用程序,需要一图表的形式显示数据,其中数据本身是动态填充.在这种情况下,可以使用Highcharts显示,使用简单的编程图表的形式的数据.

### 项目中运行(具体实施步骤):

1. Highcharts沿用了jQuery,MoolTool以及Prototype等JavaScript框架来处理基本的JavaScript任务.因此,在使用Highcharts之前,需要在页面头部引入这些脚本文件.如果你使用jQuery作为基本框架,那么需要在页面头部引入jQuery和Highcharts两个文件
2. 在网页头部的脚本标签,或在一个单独的js文件,添加JavaScript代码来初始化图表.renderTO参数用来设置图表渲染的位置,一般来说是一个具有id的div元素(参考第三步)
3. 在页面中添加一个div元素,作为放置Highcharts图表的容器.需要为其设置id值,已第二步RenderTO参数绑定.设置的宽度和高度将作为Highcharts图表的宽度和高度.
4. 你可以通过Highcharts.setOptions方法为Highcharts图表设置一个全局的主题(可选的).下载包含有四个预定义的主题,如果你需要使用这些主题,只需在highcharts.js后引用这些文件

[使用教程](https://www.hcharts.cn/docs)
[帮助文档](https://api.hcharts.cn/highcharts)