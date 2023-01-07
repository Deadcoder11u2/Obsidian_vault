When a reuqest comes it is matched with the url pattern in the servlet mapping attribue.

Basic structure of web.xml
```xml
<web-app>
	<servlet>
		<servlet-name> servletName</servlet-name>
		<servlet-class>servletClass</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>servletName</servlet-name>
		<url-pattern>*.*</url-pattern> 
	<servlet-mapping>
<web-app>
```
