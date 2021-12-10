Repository Init Content
=======================

Your project description here.

#CONNECTING JBPM WITH EXTERNAL DATABASE(MY SQL)
===============================================

connecting jbpm with external database

1.we need to open jbpm-server

2.Go to Bin folder and then goto drivers

3.copy my-sql-connector-java

4.now goto jbpm-server-7.60.0.Final-dist\modules\system\layers\base\com

5.Create a folder name mysqldatabase

6.Then create another folder mysql

7.Then create main

8.Then paste my-sql-connector-java

9.Then create module.xml file
 And copy paste the content...........

<?xml version="1.0" encoding="UTF-8"?>
<module xmlns="urn:jboss:module:1.5" name="com.mysqldatabase.mysql">

<resources>
    <resource-root path="mysql-connector-java-8.0.16.jar"/>
</resources>
<dependencies>
    <module name="javax.api"/>
    <module name="javax.transaction.api"/>
    <module name="javax.servlet.api" optional="true"/>
</dependencies>


For resource-root path:
Open my-sql-connector-java in winRar goto 

META-INF/INDEX.LIST /


There we can find resource root path
          
10.Now start jbpm and go to admin settings by clicking on      ⚙ icon in the top right corner
                                      
11. Click on service task administration.

Scroll down till the “ExecuteSQL” service task and toggle “ON” the service task.


12. Go to admin settings and Go to ⚙ icon in the top right corner
Click on data sources 
And add the driver 



And then add the data source 

The last string of the url must be the data 

source name (any datasource name present in mysql work bench)

13.Create a project
And add a business process with just a start and end nodes.

 Go to project settings –> “Service Task” –> Click “Install” for “ExecuteSQL” service task. It will ask for a data source JNDI name
To get JNDI name
Open standalone/configuration/standalone.xml

14.search for <datasource jndi-name="jndistring"........../>
The one which is not ExternalDS
Copy the jndi string present there.........

 15.Enter the JNDI name for the data source on which SQL queries would be executed. Save the settings.

16. Now open the business process and .......add "ExecuteSQL" in work items......

17. Add a process variable of type object


18. And now open the "ExecuteSQL" node and 

19. “ExecuteSqlWorkItemHandler” has 3 input parameters and 1 output parameter.

MaxResults -: 10
ColumnSeparator -: ,
SQLStatement -: select * from table_name

Result -: process variable added
20. In pom.xml add the dependency

<dependency>
      <groupId>org.jbpm.contrib</groupId>
      <artifactId>execute-sql-workitem</artifactId>
      <version>7.60.0.Final</version>
    </dependency>

21.save and deploy
