# Notes on javaDownloader

Allows equipment lists to exported from Pure and converted into OpenOrg RDF

I've zipped up the Eclipse (IDE) project that includes all the code, templates etc. including the ant build file (see attached).
The configs you need to update in the 3 files are shown below e.g. in web.xml you configure your Pure service url (probably no need to change 'equipments' part) which would then be something like http://pure.aber.ac.uk/ws/rest/equipments
The default ant build target is 'deploy' which requires the file path to root of servlet container (tomcat 7).

I'd recommend setting it up as a test on your PC and use the service URLs below.

###Service URLs
http://localhost:8080/pureEquipment/service/equipment/xml
http://localhost:8080/pureEquipment/service/equipment/html


###webContent/WEB-INF/web.xml
```xml
  <context-param>
    <param-name>pure.resource.equipment</param-name>
    <param-value>equipments</param-value>
  </context-param>

  <context-param>
    <param-name>pure.service.url</param-name>
    <param-value>http://pure.aber.ac.uk/ws/rest</param-value>
  </context-param>
```

###resources/log4j.properties
```
log4j.rootCategory=DEBUG, A1
#log4j.rootCategory=INFO, A1
log4j.appender.A1=org.apache.log4j.RollingFileAppender
#log4j.appender.A1.File=/pure/logs/pureEquipment.log
log4j.appender.A1.File=/Users/awc/dev/logs/pureEquipment.log
log4j.appender.A1.MaxFileSize=1000KB
# Keep ten backup files
log4j.appender.A1.MaxBackupIndex=10
# A1 uses PatternLayout.
log4j.appender.A1.layout=org.apache.log4j.PatternLayout
log4j.appender.A1.layout.ConversionPattern=%d [%t] %-5p %c - %m%n
```

###build.xml
```xml
<!-- deploy properties -->
<property name="servlet.container" value="/Users/awc/dev/apache/tomcat"/>
````
