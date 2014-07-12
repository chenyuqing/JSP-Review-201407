# 第四章 JSP编程技术(重点)

----------
- JSP的主要内容包括：**3大编译指令**，**7大操作指令**(课本6个)和**9大隐含对象**(课本7个)。
### 4.2 JSP页面结构(page68)
- JSP的页面主要包含3种元素：**编译指令**，**操作指令**和**JSP代码**。

	- 编译指令
		> **编译指令告诉JSP解释引擎，需要在编译时做什么动作，例如引入其他类，设置JSP页面使用什么语言编码等。**
	- 操作指令
		>**操作指令则是在JSP页面被请求时动态执行的，比如可以根据某个条件动态跳转到另一个页面。**
	- JSP代码
		>**JSP代码指我们嵌入JSP页面中的Java代码，分两种：变量和方法的声明，使用“<%!”和“%>”标记，另一种是常用到的用“<%”和“%>”包含的JSP代码块。**
<br/>

--------
### 4.3 编译指令(page68)
- JSP指令的**一般形式**：**<%@ 指令名 属性1 = "value1" %>**，**<%@ 指令名 属性2 = "value2" %>**，多个指令也可以合并写为：**<%@ 指令名 属性1 = “value1” 属性2 = "value2" %>**

- JSP的3大编译指令：**page指令**，**include指令**，taglib指令(不考)。

	- page指令：page 指令是最复杂的JSP指令，它的主要功能为设定整个JSP 网页的属性和相关功能。
		 <table>
				<tr>
					<th>属性</th>
					<th>定义</th>
				</tr>
			   <tr>
			      <td width="170">language=“语言"</td>
			      <td width="500">主要指定JSP 容器 要用什么语言来编译JSP 网页。JSP 1.2 规范中指出，目前只可以使用Java 语言，不过未来不排除增加其他语言，如C、C++、Perl 等等。默认值为Java语言 </td>      
			   </tr>
			   <tr>
			      <td>extends=“基类名"</td>
			      <td>主要定义此JSP 网页产生的Servlet 是继承哪个父类</td>     
			   </tr>
				<tr>
			      <td>import= "importList"</td>
			      <td>定义此JSP 网页可以使用哪些Java类库</td>     
			   </tr>
			   <tr>
			      <td>errorPage="error_url" </td>
			      <td>表示如果发生异常错误时，网页会被重新指向指定的URL</td>     
			   </tr>
				<tr>
			      <td>isErrorPage="true | false" </td>
			      <td>表示此JSP Page 是否为专门处理错误和异常的网页</td>     
			   </tr>
				<tr>
			      <td>contentType = "ctinfo"</td>
			      <td>表示MIME 类型和JSP 网页的编码方式，其作用相当于HttpServletResponse接口的setContentType()方法</td>     
			   </tr>
				<tr>
			      <td>isThreadSafe="true | false"</td>
			      <td>告诉JSP 容器，此JSP 网页是否能同时处理多个请求。默认值为true，如果此值设为false， 转义生成的Servlet会实现SingleThreadModel接口。</td>     
			   </tr>
				
				<tr>
			      <td>session="true | false"</td>
			      <td>决定此JSP 网页是否可以使用session 对象。默认值为true</td>     
			   </tr>
			</table>	
	- include指令(page70):用来指定怎样把另一个文件包含到当前的JSP页面中，这个文件可以是普通的文本文件，也可以是JSP页面。例如：**<%@include file="login.htm"%>**。
		> 使用include指令，**可以实现JSP页面的模块化，使JSP的开发和维护变得非常简单**。
<br/>

--------
### 4.4 操作指令(page71)
- 操作指令和编译指令不同，编译指令是通知Servlet引擎的处理消息，而**操作指令只是运行时的动作。**编译指令在将JSP编译成Servlet时起作用；而**操作指令通常可替换成JSP脚本，它只是JSP脚本的标准化写法**。

- JSP操作指令主要有如下的6个：
	1. jsp:include：用于引入静态和动态的资源，功能和include指令相同。格式：<jsp:include page="test.htm"/> 
	2. jsp:forward：执行页面转向，将请求的处理转发到下一个页面。格式：<jsp:forward page="test.htm"/>   
	3. jsp:param：用于传递参数，必须与其他支持参数的标签一起使用。 
	
		><jsp:forward page="mypage.jsp">  
		><jsp:param name="param1" value="value1"/>  
		><jsp:param name="param2" value="value2"/>  
		></jsp:forward> 
	4. jsp:useBean：创建一个JavaBean的实例。  
	5. jsp:setProperty：设置JavaBean实例的属性值。  
	6. jsp:getProperty：输出JavaBean实例的属性值
	7.   	

- JSP的操作指令均以**“/>”**结束。
		

--------
### 4.5 JSP代码(page72)
- 变量和方法(略)
- 代码块(略)

--------
### 4.6 7大隐含对象(page75)
- 隐含对象：有些对象不用声明就可以在JSP页面的脚本代码和表达式中随意使用，这些缺省对象统称为隐含对象。
- 7大隐含对象：
	- **out**		页面输出对象；
	- **request**	请求对象；
	- **response**	响应对象；
	- **application**	应用对象； 
	- **session**	会话对象；
	- **cookie**		对象；
	- **pageContext**	对象；
	
		<table>
			<tr>
				<th>对象名</th>
				<th>对象类型</th>
				<th>作用域</th>
				<th>定义</th>
			</tr>
		   <tr>
		      <td>out</td>
		      <td>JspWriter</td> 
			  <td>page</td>
		      <td>一个输出的缓冲流，给浏览器的客户返回内容</td>      
		   </tr>
			<tr>
		      <td>request</td>
		      <td>HttpServletRequest</td> 
			  <td>request</td>
		      <td>用来得到客户端的信息</td>      
		   </tr>
		   <tr>
		      <td>response</td>
		      <td>HttpServletResponse</td> 
			  <td>page</td>
		      <td>处理服务器端对客户端的一些响应</td>      
		   </tr>
			<tr>
		      <td>application</td>
		      <td>ServletContext</td> 
			  <td>application</td>
		      <td>用来保存网站的一些全局变量</td>      
		   </tr>
		   <tr>
		      <td>session</td>
		      <td>HttpSession</td> 
			  <td>session</td>
		      <td>用来保存单个用户访问时的一些信息</td>      
		   </tr> 
			<tr>
		      <td>cookie</td>
		      <td>Cookie</td> 
			  <td>不清楚呢</td>
		      <td>将服务器端的一些信息写到客户端的浏览器中</td>      
		   </tr> 
			<tr>
		      <td>pageContext</td>
		      <td>PageContext</td> 
			  <td>page</td>
		      <td>提供了访问和放置页面中共享数据的方式</td>      
		   </tr>   
		</table>

--------
### 4.7 response对象(page76)	
- 网页转向：sendRedirect()方法，跳转到其他页面
	>格式：response.sendRedirect("URL 地址");
- 与<jsp:forward>的最大区别
	>使用<jsp:forward>只能在本站内跳转，但用response.sendRedirect("URL 地址")可以跳转到任何一个地址的页面。

- 其他(略，自己看书)


--------
### 4.8 request对象(page78)
- 自己看书