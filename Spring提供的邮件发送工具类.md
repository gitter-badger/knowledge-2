## Spring提供的邮件发送工具类

### 配置

ApplicationContext.xml中注册Spring提供的邮件发送工具类


```
<!-- spring框架提供的用于发送邮件的工具类 -->
	<bean id="mailSender" class="org.springframework.mail.javamail.JavaMailSenderImpl">
		<!-- 邮件服务器 -->
		<property name="host" value="smtp.163.com"></property>
		<!-- 发件人邮件地址 -->
		<property name="username" value="b5jem93iyilian@163.com"></property>
		<!-- 发件人邮箱密码 -->
		<property name="password" value="abcd1234"></property>
		<property name="javaMailProperties">
			<props>
				<prop key="mail.smtp.host">smtp.163.com</prop>
				<prop key="mail.transport.protocol">smtp</prop>
				<prop key="mail.smtp.auth">true</prop>
			</props>
		</property>
	</bean>
```

### 应用

```
public class SendMessage {
	//注入发送邮件的对象
	@Autowired
	private JavaMailSenderImpl mailSender;
	
	public void send() throws Exception {
		MimeMessage msg = mailSender.createMimeMessage();
		MimeMessageHelper helper = new MimeMessageHelper(msg, true, "UTF-8");
		//设置发件人地址,ApplicationContext.xml中设置的username
		helper.setFrom(mailSender.getUsername());
		//设置收件人地址,可改成动态邮箱地址
		helper.setTo("test@itcast.cn");
		//设置邮件主题
		helper.setSubject("这是一个富文本邮件");
		// MimeMessageHelper第二个参数true，表示text的内容为html
		//<img/>标签，src='cid:file'，'cid'是contentId的缩写，'file'是一个标记，需要在后面的代码中调用MimeMessageHelper的addInline方法替代成文件
		helper.setText("<!DOCTYPE html><html><body>"
				+ "<table border='0.5' style='width: 99%'>"
				+ "<tr>"
				+ "<td>这是一个表格</td>"
				+ "</tr>"
				+ "</table>"
				+ "<img src='cid:file'/></body></html>", true);
		//图片的绝对路径
		//FileSystemResource file = new FileSystemResource("d:\\1.png");
		//图片的相对路径
		ClassPathResource file = new ClassPathResource("1.png");
		helper.addInline("file", file);
		mailSender.send(msg);
	}
}

```

