
# Manorrock Oyena Action

The Manorrock Oyena Action module delivers you with an action framework that you
can use with Eclipse Mojarra.

## Prerequisites

Your project should already be configured to use Eclipse Mojarra.

## Configuration

To use it in your web application you will need to do the following:

1. Add the Maven dependency
2. Add a faces-config.xml with the CdiLifecycleFactory
3. Add a beans.xml
4. Add a Servlet mapping for the Oyena Action Servlet

### Add the Maven dependency

Add the following Maven dependency:

    <dependency>
      <groupId>com.manorrock.oyena</groupId>
      <artifactId>oyena-action</artifactId>
      <version>x.y.z</version>
    </dependency>

Where you need to replace x.y.z with the version you want to use.

### Add a faces-config.xml with the CdiLifecycleFactory

And you need to have a faces-config.xml in the WEB-INF directory with at minimum the following:

    <faces-config version="2.3"
              xmlns="http://xmlns.jcp.org/xml/ns/javaee"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
                                  http://xmlns.jcp.org/xml/ns/javaee/web-facesconfig_2_3.xsd">
      <factory>
        <lifecycle-factory>com.manorrock.oyena.cdi.CdiLifecycleFactory</lifecycle-factory>
      </factory>
    </faces-config>

### Add a beans.xml

As the framework requires CDI you need to activate CDI.

Add an placeholder beans.xml to the WEB-INF directory and it will take care of that:

    <beans
        xmlns="http://xmlns.jcp.org/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
                            http://xmlns.jcp.org/xml/ns/javaee/beans_2_0.xsd"
        bean-discovery-mode="all">
    </beans>

### Add a Servlet mapping for the Oyena Action Servlet

Add a servlet mapping to the web.xml file:

    <web-app xmlns="http://java.sun.com/xml/ns/javaee"
	 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
	 version="4.0">
      <servlet-mapping>
        <servlet-name>Oyena Action Servlet</servlet-name>
        <url-pattern>/*</url-pattern>
      </servlet-mapping>
    </web-app>

## Using it

To actually use it you wil need to create 2 components.

1. Create a CDI bean
2. Create a Facelet page

### Create a CDI bean

Create a CDI bean with the following content and use your IDE to resolve the
necessary imports:

    @RequestScoped
    public class IndexPageBean implements Serializable {
 
      /**
       * Execute the page.
       * 
       * @return /index.xhtml
       */
      @ActionMapping("/index")
      public String execute() {
        return "/index.xhtml";
      }
    }

### Create a Facelet page

Create the /index.xhtml Facelet page in the root of your web application with the 
following content:

    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
      "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

    <html xmlns="http://www.w3.org/1999/xhtml"
          xmlns:h="http://xmlns.jcp.org/jsf/html">
      <h:head>
        <title>Index page</title>
      </h:head>
      <h:body>
        Hello from there!
      </h:body>
    </html>

## Try it

Deploy the web application to the server of your choice.

Assuming the web application is deployed at /myaction on your localhost server
listening on port 8080 you would browse to http://localhost:8080/myaction/index
to try it.

Enjoy!
