# J2EE

[Java procesy (JVM) obecne](../sw/java.html)  
[Programovani v java obecne](../dev/java.html)  

### Webove aplikace

[Zdrojove kody aplikace Timesheet.war](ftp://ftp.linuxjournal.com/pub/lj/listings/issue197/10810.tgz)

==Zakladni servlet Hello:==

```
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class Hello extends HttpServlet {
  public void doGet(HttpServletRequest request, HttpServletResponse response)
  throws ServletException, IOException {
    PrintWriter out = response.getWriter();
    out.println("Hello");
  }
}
```
  
javac -classpath /usr/share/tomcat6/lib/tomcat6-servlet-2.5-api-6.0.26.jar -d /usr/share/tomcat6/webapps/WEB-INF/classes/ Hello.java

==Servlet HelloHtml:==

```
package www1; // nazev adresare, do ktereho se to pak zkompiluje

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class HelloHtml extends HttpServlet {
  public void doGet(HttpServletRequest request, HttpServletResponse response)
  throws ServletException, IOException {
    response.setContentType("text/html");
    PrintWriter out = response.getWriter();
    String docType = "&lt;!DOCTYPE HTML PUBLIC \"=//W3C/DTD HTML 4.0" +
      "Transitional//EN\"&gt;\n";
    out.println(docType + "&lt;HTML&gt;\n" +
      "&lt;HEAD&gt;&lt;TITLE&gt;Hello HTML&lt;/TITLE&gt;&lt;/HEAD&gt;" +
      "&lt;BODY&gt;\n&lt;H1&gt;Hello&lt;/H1&gt;\n" +
      "&lt;/BODY&gt;&lt;/HTML&gt;");
  }
}
```
