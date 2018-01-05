## excel读写工具-POI
### 介绍

目前常见读写Excel的工具类开源JavaAPI有两种方式

1. JXL(Java Execl API) [官方网站](http://jexcelapi.sourceforge.net/)
2. Apache的POI(Poor Obfuscation Implementation) [官方网站](http://poi.apache.org)

* POI支持微软的OLE2格式文件Office2003及以下版本,同时支持微软OOXML(Office Open XML)标准,也就是Office2007以上版本.JXL只能实现对Excel2003以下版本的支持.

* POI使用HFFS对象操作OLE2格式Excel,文件后缀为.xls的;使用XSSF,SXSSF对象操作OOXML格式Excel,文件后缀为.xlsx的.

* 对于OLE2版本的Excel,一个Sheet工作表它的行最多支持到65536行,列支持到256列;

* 对于OOXML版本的Excel,一个Sheet工作表它的行最多支持到1048576行,列支持到65536列.

### 核心API

新建工作簿

```
HSSFworkbook wb = new HSSFworkbook();
```

打开工作簿

```
HSSFworkbook wb = new HSSFworkbook(new FileInputStream(xlsFile));
```

建立新的sheet对象

```
HSSFSheet sheet = wb.createSheet("我的第一个工作簿");
```

选择第一个工作簿

```
HSSFSheet sheet = wb.getSheet(0);
```

设置工作簿的名称

```
wb.setSheetName(0,"我的第一个工作簿");
```

创建行对象

```
HSSFRow nRow = null;
nRow = sheet.createRow(1);//第二行
```

指定列 创建单元格对象

```
HSSFCell nCell = null;
nCell = nRow.createCell((short)(2));//第三列
```

指定列 创建单元格对象

```
nCell.setCellValue("我是单元格"); 
```

设置样式 注意:样式不能重复设置

```
nCell.setCellStyle(leftStyle(wb));
```


### POI读写大数据量EXCEL

有三种模式:

1. eventmodel方式,基于事件驱动,SAX的方式解析Excel(.xlsx是基于OOXML的),CPU和内存消耗非常低,但是只能读不能写

2. usermodel,就是我们一般使用的方式,这种方式可以读写,但是CPU和内存消耗非常大

3. SXSSF,POI3.8以后开始支持,这种方式只能写Excel

采用的读取方式是事件模型eventusermodel,因为Excel2007采用的存储方式实际上是**xml**形式Excel2007可以用系统自带的解压缩软件解压之后可以看到数据都是存储成**xml**格式的数据,所以这里采用**sax**的方式对Excel文件进行解析.

### 应用(查询数据库,导出一个Excel表格)

```
public String export() throws Exception{
		//查询数据库中的所有数据
		List<SubArea> list = service.findAll();
		
		//创建一个Excel文件（在服务器内存中）
		HSSFWorkbook excel = new HSSFWorkbook();
		//在表格中创建一个工作簿
		HSSFSheet sheet = excel.createSheet("分区数据");
		//在工作簿中创建行
		HSSFRow title = sheet.createRow(0);
		//在行中创建单元格
		title.createCell(0).setCellValue("分区编号");
		title.createCell(1).setCellValue("分区关键字");
		title.createCell(2).setCellValue("分区辅助关键字");
		title.createCell(3).setCellValue("分区位置信息");
		title.createCell(4).setCellValue("区域信息");
		
		//遍历集合，获取分区数据，写入表格
		for (SubArea subArea : list) {
			HSSFRow data = sheet.createRow(sheet.getLastRowNum() + 1);
			data.createCell(0).setCellValue(subArea.getId());
			data.createCell(1).setCellValue(subArea.getKeyWords());
			data.createCell(2).setCellValue(subArea.getAssistKeyWords());
			data.createCell(3).setCellValue(subArea.getAddress());
			data.createCell(4).setCellValue(subArea.getArea().getName());
		}
		
		//基于输出流将Excel文件下载到客户端浏览器（一个流、两个头）
		ServletOutputStream out = ServletActionContext.getResponse().getOutputStream();
		
		String filename = "分区数据.xls";
		String agent = ServletActionContext.getRequest().getHeader("User-Agent");
		filename = FileUtils.encodeDownloadFilename(filename, agent);
		
		//设置头信息
		ServletActionContext.getResponse().setContentType("application/vnd.ms-excel");
		ServletActionContext.getResponse().setHeader("content-Disposition", "attachment;filename=" + filename);
		
		excel.write(out);
		
		return NONE;
	}

```

