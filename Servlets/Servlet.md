Some knowledge about CGI(common gateway interface)
CGI is platforom dependent
For each and every request a new process and created
hence forth response timer is higher

1. We can put jar file in lib foler
2. Web server serves only static page
3. NOTE: DD stands for deployment descriptor
4. Apache HTTP server is not a application server
5. JRun is a application server
6. Glass fish is a application server
7. Glass fish is not a web server
8. Life cycle of servlet is controlled by container
9. HTML page is static
10. There is not limit for DD per one web application
11. web.xml file should be put in WEB-INF


Important mappings of web.xml file

1. servlet-mapping tag of DD maps the servlet with the url pattern
2. service() method is called when client request come?
3. There is one ServletContest per servlet
4. Life-cycle methods of servlet that can be over-ridden 
	a. service
	b. init
	c. destroy
5. Servlet interface contains the servlet life cycle methods
6. There is one servlet-config per application
7. The destroy life cycle method make ready servlet for garbage collection
8. Get Http method is idempotent
9. Init life cycle method is called only once in servlet life
10. Init methods doesn't exists in HttpServlet Class.
11. response.addHeader() -> add a new header if that is not existing, otherwise replace the value
12. Which method will decide which method to call i.e. doGet or doPost -> **Service**
13. Forward method redirect to resources to different servers internally
14. response.setHeader() Add a new header and value or add an additional value to the existing header
15. response.setIntHeader() Replace the value to integer to existing header or Add a new header with integer value
16. redirect method always sends a header back to the client to get the desire page
17. doTrace method show the client what server is recieving



## 

1. Servlet is not a stand alone application
2. You have to put your web application in webapps folder of tomcat
3. we can defince the servlet context through context-param tag
4. The init parameters are read by container when the servlet is initialised
5. We can define servlet config in web.xml through init-param
6. We can send only 1024 characters through doGet()
7. 

## Ways we can get servlet context
a. getServletConfig().getServletContext().getInitParameter()
b. getServletContext().getInitParameter()
c. this.getServletConfig().getInitParamenter()



Life cycle of Servlet

- Load Servlet class
- Create servlet instance
- Call init() method
- Call service() method
- Call destroy() method


Load Servlet Class: Web container lads the servlet when the first request is received. This step is executed only once at the time of first request.

Create servlet instance: After loading the servlet calss web container creats teh servlet isntance. Only one instance is created for a servlet and all concurrent requests are executed on the same servlet instance.

Call init() method: After creating the servlet instance web container calls the servlets's init method. This methos is used to initilalize the servlet before processing first request. It is called once by the web container.

Call service() method: After initialization process web container calls service method. Service method is called for every reqyest. For every reqyest servlet creates a seperate thread.

Call destroy() method: This method is called by web container before removing the servlet instance. Destroy method asks serlet to releases all the resources associated with it. IT so called only once by the web container when all threads of the servlet have exited or in a timeout case.
There exists a Servlet interface that we can extend to implement a servlet of our own.
Web.xml is deployment descriptor
Generic Servlet class in java

```CQL
SELECT * FROM TABLE;
```