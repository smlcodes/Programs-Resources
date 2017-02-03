HYGIEIA DASHBOARD 

MONGO DB INSTALLATION
Know your PC Architecture, Open Command prompt and run below command 
C:>wmic os get osarchitecture

1) DOWNLOAD MONGODB
There are three builds of MongoDB for Windows:
1) MongoDB for Windows Server 2008 R2 edition [Download link]
2) MongoDB for Windows 64-bit [Download link]
3) MongoDB for Windows 32-bit [Download link]

2) EXTRACT AND CREATE FOLDERS
•	download zip files which you extract directly onto any place in your system of your choice
•	 I have extracted them in “d:/mongodb“. 
Also, please create following directories inside d:/mongodb
•	D:\mongodb\data
D:\mongodb\log

3) PATH AND INSTALLATION
  
MongoDB = D:\mongodb				D:\mongodb\bin
4. CREATE A MONGODB CONFIG FILE
 it’s just a text file, for example: d:\mongodb\mongo.config
d:\mongodb\mongo.config
##store data here
dbpath=D:\mongodb\data

##all output go here
logpath=D:\mongodb\log\mongo.log

##log read and write operations
diaglog=3

4) START/SHUTDOWN THE MONGODB SERVER
Start: Run below command in command prompt

C:\mongodb\bin>mongod –dbpath=D:/mongodb

d:\mongodb\bin>mongod.exe --config="D:\C_Drvie_ Mongo\mongo.config"
d:\mongodb\bin>mongod.exe --config="D:\mongodb\mongo.config"
 
Running Commands 
	mongo

 

Shutting Down
	db.shutdownServer()

5. CONFIGURE TO HYGIEIA
1.	Run the following commands as shown below at mongodb command prompt  /usr/bin/mongodb-linux-x86_64-2.6.3/bin/mongo 
	 mongo  
MongoDB shell version: 3.0.4
connecting to: test  
 

	use dashboarddb
switched to db dashboarddb

$ mongo  
MongoDB shell version: 3.0.4
connecting to: test  

> use dashboarddb
switched to db dashboarddb
> db.createUser(
        {
          user: "dashboarduser",
          pwd: "dashboarduser",
          roles: [
             {role: "readWrite", db: "dashboarddb"}
                  ]
          })
      ```
Run Direct

CONFIGURING HYGIEIA 

1.	Download Hygieia 1.5.0 
https://github.com/capitalone/Hygieia/releases/tag/Hygieia-1.5.0


2.	Change / add Settings.xml file at C:\apache-maven-3.3.9\conf

  <mirrors>    
      <mirror>
                       <id>internal-repository</id>
                       <name>Maven Repository Manager running on http://vblrqtools-32</name>
                       <url>http://vqtools114/nexus/content/groups/PUBLIC_REPO/</url>
                       <mirrorOf>*</mirrorOf>
    </mirror>
  </mirrors>
3.	Extract and Open folder and run maven Build
 
Open command prompt and go to Hygieia folder and run mvn cmds as below
mvn clean install package
mvn clean install package -Dmaven.test.skip=true
(or –for Skipping PDM Violations)
mvn clean install package -Dmaven.test.skip=true -Dpmd.failOnViolation=false

If UI Throws Error Don’t Worry…….
It will take some time wait …………., after complete open Eclipse
1.	CONFIGURE MAVEN IN ECLIPSE
Copy maven installation path (Ex. C:\apache-maven-3.3.9)
Window  preferences  Maven  Installations == add maven path
 
 
Change Settings.xml file path Window  preferences  Maven  User Settings 
ss 

2.	IMPORT CODE TO ECLIPSE
File  	Import		Maven 	Existing Maven Projects, browse Downloaded Hygieia folder
 

You will get Project like below
 
Select all  Right click  Maven Update
If Errors in pom.xml take it Lite
api project  right click new File : 
 
dbname=dashboarddb
#dbusername=[MogoDb Database Username, defaults to empty]
#dbpassword=[MongoDb Database Password, defaults to empty]
dbhost=localhost
dbport=27017

api project  Go to src  com.capitalone.dashboard.Application.java Rightclick
Run Configuartions  Java Application  go to arguments  program args : add
--spring.config.location=dashboard.properties
 
Apply
If any errors Check Database name /
 check com.capitalone.dashboard.config.MongoConfig.java
    @Value("${dbname:dashboarddb}")
    private String databaseName;
    @Value("${dbhost:localhost}")
    private String host;
    @Value("${dbport:27017}")
    private int port;
    @Value("${dbusername:}")
    private String userName;
    @Value("${dbpassword:}")
    private String password;
3.	CONFIGURING NODEJS
Install GIT First, 
Open NodeJs Commond line
Run npm command 

•	Run below commands one by one / You can refer
npm install -g bower
npm install -g gulp

•	Go to Hygieia root folder and go to UI folder from command line
For me it is  cd D:\POC\Hygieia-Hygieia-1.5.0\Hygieia-Hygieia-1.5.0\UI

Run below command
npm install
npm install -g bower
npm install -g gulp
npm install

4.	IF ANY ISSUES
Configuring "bower" , "git", "npm" behind infosys firewall:

Prerequisites:
Install npm , and git (select option to put git in path)

Steps:
1. Double check if git is in command line path, open a command prompt and type git to confirm.
2. Under start menu, you will see "node js command prompt", open it, you will go to C:\users\<your user id>.
          a) Run "notepad .npmrc" , and enter the below contents there




%5C is "url-encoded" string for "\" character. If your password has special characters , it is better to url encode them. Please check below link for url encoded characters.
http://www.w3schools.com/tags/ref_urlencode.asp

1.	For first time git setup, run below commands 
$ git config --global user.name "John Doe" 
$ git config --global user.email johndoe@example.com

2.	Run "notepad .gitconfig" and paste/add the below contents



3.	Run "notepad .bowerrc" and paste the below contents


4.	 Due to a bug in npm (may be solved in later versions), we have to manually create "npm" folder under "C:\Users\YOUR_USER_ID\AppData\Roaming"

5.	RUN COMMANDS ON NODEJS COMMANDLINE
1.	Install GIT and set PATH 
If Git not found Set PATH = C:\Program Files\Git\bin;.
Check git –version 
 

2.	Run below commands on normal command prompt to install all
npm install -g bower  
npm install -g gulp

3.	Open NodeJs cmd navigate to UI Folder
npm install
bower install
 

Check Status
>bower --version
	>Git --version
 


Navigate to UI folder of the Hygieia through NodeJs commndline
gulp serve					 It will start the dashboard






WORKING WITH HYGIEIA
1.	STARTING UI
•	Start MongoDB Server
cd d:\mongodb\bin
mongod.exe --config="D:\mongodb\mongo.config"
mongo			 using other command line 

•	Run API project

Eclipse  Api  Run  Java Application  Application.java arguments
--spring.config.location=dashboard.properties

•	Start UI 
Open NodeJS command line, navigate to UI Folder, type
	gulp serve
 
2.	STARTING COLLECTORS
1.	STARTING JENKINS-BUILD-COLLECTORS
o	Go to https://github.com/capitalone/Hygieia
o	Open https://github.com/capitalone/Hygieia/tree/master/jenkins-build-collector
o	It will have Sample application.properties file details
o	Open Project
o	Create  new File  application.properties 
o	Copy data from Github file to local application.properties
#Database Name 
dbname=dashboarddb

#Database HostName - default is localhost
#dbhost=localhost

#Database Port - default is 27017
#dbport=9999

#Database Username - default is blank
#dbusername=db

#Database Password - default is blank
#dbpassword=dbpass

jenkins.servers[0]=http://localhost:8181/jenkins/
#Collector schedule (required)
jenkins.cron=0 0/1 * * * *

#Jenkins server (required) - Can provide multiple

#If using username/token for api authentication (required for Cloudbees Jenkins Ops Center) see sample
#jenkins.servers[1]=http://username:token@jenkins.company.com

#Another option: If using same username/password Jenkins auth - set username/apiKey to use HTTP Basic Auth (blank=no auth)
#jenkins.username=
#jenkins.apiKey=

#Determines if build console log is collected - defaults to false
jenkins.saveLog=true
o	Right click on Project  Run As  Run configurations  Run Applciation.java
o	Open  Higieia dashboard on webpage
o	Click on Configure Build Widget  select Jenkins/Hudson save
o	It will display Jenkins  data
MISCELLANEOUS
1. SPRING EXPRESS CONFIGURATION
1.	Download https://github.com/andzdroid/mongo-express
2.	Copy config.default change name to config.js
3.	Open NodeJs Command line
To install:
npm install -g mongo-express
Or if you want to install a non-global copy:
npm install mongo-express
4.	By default config.default.js is used where the default authentication is admin:pass

5.	Go to root folder, run below command 
npm install -g mongo-express

6.	To Start 
7.	D:\Softwares\mongo-express-0.29.10\mongo-express-0.29.10>
mongo-express -u admin -p pass -d db 
Open: http://localhost:8081/   It’s ready
3.	ADMINMONGO

Download: https://github.com/mrvautin/adminMongo
1.	Install dependencies: npm install
2.	Start application: npm start
3.	Visit http://127.0.0.1:1234 in your browser
4.	Local Host Configure : mongodb://localhost:27017
 
CODE FLOW OF EXECUTION
•	Combo box loads Jobs
•	Select one Job
•	Get the URL of that Job
•	Get the JSON of that URL
•	Repeat loop and get the elements
•	Save in DB
•	Call API Url to Retrieve saved data
HYGIEIA VERIZON MODULES
1.	UTF-Collector
2.	Service Virtualization
3.	Dynatrace  

Every collector contains 4 modules
1.	UI
2.	API
3.	Core
4.	Collector

For API, UI & Core are common for all collectors. Only small changes for specific controllers.
 First we will see the common API & UI, working then we will go to specific collector implementations.
UI
You can refer how we configure UI in Previous steps. 
1.	For running UI, we must Start API. After API starts the browser displays UI as below
 

2.	After Login the dashboard displays as below
 

3.	Click on Create Dashboard for adding new dashboard and fill details.  

4.	After create, the Dashboard displays as below 

5.	We configure any widget by clicking on Configure widget

API

Here API is work as an Interface between Collector and UI
It contains the Controller classes, which helps to UI which Collector logic has to be execute whenever request comes from UI 
API module contains following major packages
Root Folder is  com.capitalone.dashboard
•	Request	 this package classes are used to store Request details 
•	Rest	 this package classes contains Controller classes 
Ex :  @RequestMapping(value = "/apm", method = POST, produces = APPLICATION_JSON_VALUE)

•	Service  	this package classes are used for send response to UI

Apart from these API specific calls are configured in UI below folder
\UI\src\components\widgets
In this folder every widget specific calls are configured  
Ex :   
CORE
It will contains all model classes for all collector’s 

I.	UTF-COLLECTOR
1.	API
UFTController.java
All controller specific logics are configured here.
 
    @RequestMapping(value = "/TestResults", method = GET, produces = APPLICATION_JSON_VALUE)
    public DataResponse<Iterable<TestResult>> builds(@Valid UFTRequest request) {

		return uftService.search(request);
    }
    
    @RequestMapping(value = "/TestResults/Interface", method = GET, produces = APPLICATION_JSON_VALUE)
    public DataResponse<Iterable<TestResult>> interfaceBuilds(@Valid UFTRequest request) {
    	request.setType(ResultType.SIT);
		return uftService.search(request);
    }
     
    @RequestMapping(value = "/TestResults/Functional", method = GET, produces = APPLICATION_JSON_VALUE)
    public DataResponse<Iterable<TestResult>> functionalBuilds(@Valid UFTRequest request) {
    	//System.out.println("Functional");
    	request.setType(ResultType.Functional);
    	//System.out.println("Result : "+uftService.search(request).getResult());
		return uftService.search(request);
    }
    

UFTRequest.java
All Request Details will store here
 

UFTService.java,UFTServiceImpl.java
HTTP Response logics are implemented here
  

2.	UTF-COLLECTOR 
Root folder is utf-collector/src/main/java/com/capitalone/dashboard
•	 

Collector – Package classes 
This package contains all collector specific implementations

1.	UFTTestResultCollectorTask.java
 	This the core class in this collector. On Starting collector collect() method will execute.
It contains method calls which performs Collector Specific implementation’s 

2.	UFTDefaultTestResultClient.java

This class contains collector specific implementation methods. 
List of methods:
getInstanceJobs(instanceUrl) 			 to get all the jobs from Jenkins url.
addNewJobs(buildsByJob.keySet(), collector)	 checks/adds new Jobs to DB
addNewBuilds(enabledJobs(collector, url), builds) adding new builds to DB
addTestResults(enabledJobs(collector, instanceUrl), buildsByJob);
	Adding test results to DB

3.	UFTTestResultsSettings.java
We will declare all configuration details in application.properties . this class is used to read 
those details 
application.properties (Sample)

#Database Name 
dbname=dashboarddb

#Database HostName - default is localhost
#dbhost=localhost

#Database Port - default is 27017
#dbport=9999

#Database Username - default is blank
#dbusername=db

#Database Password - default is blank
#dbpassword=dbpass

jenkins.servers[0]=http://ekyfrdcda12.ebiz.verizon.com:9003/jenkins/
#jenkins.servers[0]=http://localhost:8181/jenkins/
#Collector schedule (required)
jenkins.cron=0 0/1 * * * *
 
jenkins.saveLog=true

Model – Package classes 
	 This package contains all model classes which are used by collector package classes
UFTTestResultCollector.java
UFTTestResultJob.java

Repository – Package classes 
This package contains DB Specific classes
IUFTTestResultCollectorRepository.java
IUFTTestResultJobRepository.java

After running collector, data is stored in DB as below
 
 

 
3.	UI
1.	Create new Dashboard
 

2.	After Running API the Dashboard is display widgets as below
 

3.	Configure Test Result widget 

4.	Test Results  display as below
 



II.	SERVICE VIRTUALIZATION COLLECTOR
1.	API
ServiceVirtualizationController.java
All controller specific logics are configured here.
 

ServiceVirtualizationRequest.java
All Request Details will store here
 

ServiceVirtualizationServiceImpl.java
HTTP Response logics are implemented here
  

2.	PQ-SERVICE-VIRTUALIZATION
Root folder is pq-ServiceVirtualization/src/main/java/com/capitalone/dashboard

Collector – Package classes 
This package contains all collector specific implementations

ServiceVirtualizationtCollectorTask.java
 	This the core class in this collector. On Starting collector collect() method will execute.
It contains method calls which performs Collector Specific implementation’s 

ServiceVirtualizationClient.java

This class contains collector specific implementation methods. 
List of methods:
getInstanceJobs(instanceUrl) 			 to get JSON data from Jenkins url.
addNewJobs(buildsByJob.keySet(), collector)	 checks/adds new Jobs to DB
 addServicesaddServices(jsonObject, instanceUrl,collector);
	Adding services results to DB

ServiceVirtualizationSettings.java
We will declare all configuration details in application.properties . this class is used to read 
those details 

application.properties (Sample)

#Database Name 
dbname=dashboarddb

#Database HostName - default is localhost
#dbhost=localhost

#Database Port - default is 27017
#dbport=9999

#Database Username - default is blank
#dbusername=db

#Database Password - default is blank
#dbpassword=dbpass

svcvrtl.servers[0]=http://devtest.verizon.com:1505/
svcvrtl.servers[1]=http://devtest2.verizon.com:1505/
#svcvrtl.servers[0]=http://localhost:8181/jenkins/
#Collector schedule (required)
svcvrtl.cron=0 0/1 * * * *

 
svcvrtl.username=Username
svcvrtl.password=pass
svcvrtl.apiKey=Verizon@3
#svcvrtl.apiKey=

svcvrtl.configdays=7

#Determines if build console log is collected - defaults to false
svcvrtl.saveLog=true

Model – Package classes 
	 This package contains all model classes which are used by collector package classes
ServiceVirtualizationCollector.java
ServiceVirtualizationJob.java
Repository – Package classes 
This package contains DB Specific classes
ServiceVirtualizationRepository.java

After running collector, data is stored in DB as below 
 

 
3.	UI
5.	Create new Dashboard
 

6.	After Running API the Dashboard is display widgets as below
 

7.	Configure Service Virtualization  widget  

8.	Test Results  display as below
 

 

 
III.	DYNATRACE COLLECTOR
1.	API
PQApmController.java
All controller specific logics are configured here.
 

PQApmRequest.java
All Request Details will store here
 

PQApmServiceImpl.java
HTTP Response logics are implemented here
  

2.	PQ-DYNATRACE-COLLECTOR
Root folder is pq-dynatrace-collector/src/main/java/com/capitalone/dashboard

Collector – Package classes 
This package contains all collector specific implementations

PQApmCollectorTask.java
 	This the core class in this collector. On Starting collector collect() method will execute.
It contains method calls which performs Collector Specific implementation’s 

PQApmClient.java

This class contains collector specific implementation methods. 
List of methods:
addNewApplication(getEnvironments(pqApmApp), collector); 
updateDatas(enabledApplications(collector, pqApmApp));


PQApmSettings.java
We will declare all configuration details in application.properties . this class is used to read 
those details 

application.properties (Sample)

#Database Name
spring.data.mongodb.database=dashboarddb

#Database HostName - default is localhost
spring.data.mongodb.host=127.0.0.1

#Database Port - default is 27017
spring.data.mongodb.port=27017

#Database Username - default is blank
spring.data.mongodb.username=dashboarduser

#Database Password - default is blank
spring.data.mongodb.password=1qazxSw2

#Collector schedule (required)
pqapm.cron=0 0/1 * * * *


#Queue manager and HostName/Port specified in formt mqapp#queuemanager#host#ip
#Queue manager and HostName/Port specified in formt mqapp#queuemanager#host#ip
#Queue manager and HostName/Port specified in formt mqapp#queuemanager#host#ip
pqapm.apps[0]=ProQuest
pqapm.apps[1]=SampleApp
pqapm.envs[0]=ProQuest#PQ-SIT#mallasw#Verizon@1!#https://fetompa08.vzbi.com:8021/rest/management/reports/create/PQ SITC User Experience Metrics?type=XML&format=XML+Export
pqapm.envs[1]=ProQuest#PQ-PROD#pqdev#pqdev123#https://fetompa01vip.verizon.com:8021/rest/management/reports/create/PQ Prod User Experience Metrics?type=XML&format=XML+Export
pqapm.envs[2]=ProQuest#PQ-SITG#mallasw#Verizon@1!#https://fetompa08.vzbi.com:8021/rest/management/reports/create/PQ SITC User Experience Metrics?type=XML&format=XML+Export
pqapm.envs[3]=SampleApp#PQ-SIT#mallasw#Verizon@1!#https://fetompa08.vzbi.com:8021/rest/management/reports/create/PQ SITC User Experience Metrics?type=XML&format=XML+Export
pqapm.envs[4]=SampleApp#PQ-PROD#pqdev#pqdev123#https://fetompa01vip.verizon.com:8021/rest/management/reports/create/PQ Prod User Experience Metrics?type=XML&format=XML+Export
pqapm.envs[5]=SampleApp#PQ-SITG#mallasw#Verizon@1!#https://fetompa08.vzbi.com:8021/rest/management/reports/create/PQ SITC User Experience Metrics?type=XML&format=XML+Export
#chart names, remove spaces in name if any
pqapm.charts=TopUserActions#NumberofMilestonesReached

Model – Package classes 
	 This package contains all model classes which are used by collector package classes
PQApmCollector.java
PQApmJob.java
Repository – Package classes 
This package contains DB Specific classes
PQApmRepository.java

After running collector, data is stored in DB as below 
 
 

3.	UI
9.	Create new Dashboard
 

10.	After Running API the Dashboard is display widgets as below
 

11.	Configure Dynatrace  widget  

12.	Data as display as below
 

 


IV.	PROQUEST DEPLOY COLLECTOR
API

DeployController.java
All controller specific logic is configured here.

 


DeployServiceImpl.java
HTTP Response logic is implemented here
  

Repositories:
This repository is an interface defined to access the data. Spring Data repositories usually extend from the Repository or Crud Repository interfaces. If you are using auto-configuration, repositories will be searched from the package containing your main configuration class.

   
PROQUEST-DEPLOYMENT-COLLECTOR
Root folder is proquest-deployment-collector /src/main/java/com/capitalone/dashboard

Collector – Package classes 
This package contains all collector specific implementations

4.	PQDeployCollectorTask.java
 	This the core class in this collector. On Starting collector collect() method will execute.
It contains method calls which performs Collector Specific implementation’s 

5.	DefaultPQDeployClient.java
This class contains collector specific implementation methods. 
List of methods:
getApplications (instanceUrl) 			
To get all the jobs from Jenkins url.
getEnvironments(PQDeployApplication application)
	To get Environment details
getApplicationSettings(String envName)
To get Application details

public List<EnvironmentComponent> getEnvironmentComponents(
            PQDeployApplication application, Environment environment)
	To get Environment component details

getEnvironmentResourceStatusData()
To get Resources Status details


6.	PQDeploySettings.java
We will declare all configuration details in application.properties . this class is used to read those details  
#Database Name 
dbname=dashboarddb

#Database HostName - default is localhost
#dbhost=localhost

#Database Port - default is 27017
#dbport=9999

#Database Username - default is blank
#dbusername=db

#Database Password - default is blank
#dbpassword=dbpass


#Collector schedule (required)
pqdeploy.cron=0 0/1 * * * *

#UDeploy server (required) - Can provide multiple
pqdeploy.servers[0]=DITA
pqdeploy.servers[1]=DITC
pqdeploy.servers[2]=DITG
pqdeploy.servers[3]=SITA
pqdeploy.servers[4]=SITC
pqdeploy.servers[5]=SITG
pqdeploy.servers[6]=EKYSITA
pqdeploy.servers[7]=EKYSITB
pqdeploy.servers[8]=MIGSITG
pqdeploy.servers[9]=STAGING
pqdeploy.servers[10]=PRODUCTION
#UDeploy user name (required)
pqdeploy.username=CW_RO
#UDeploy password (required)
pqdeploy.password=cwReadOnly
#UDeploy EnvDB (required)

pqdeploy.envdb[0]=DITA#ekyfddd1scan.ebiz.verizon.com#1800#PQDITA
pqdeploy.envdb[1]=DITG#ekyfddd1scan.ebiz.verizon.com#1800#PQDITG
pqdeploy.envdb[2]=DITC#ekyfddd1scan.ebiz.verizon.com#1800#PQDITC
pqdeploy.envdb[3]=SITA#ekyfddd1scan.ebiz.verizon.com#1800#PQSITA
pqdeploy.envdb[4]=SITG#ekyfddd1scan.ebiz.verizon.com#1800#PQSITG
pqdeploy.envdb[5]=SITC#ekyfddd1scan.ebiz.verizon.com#1800#PQSITC
pqdeploy.envdb[6]=MIGSITB#omzgrid114scan.vzbi.com#1800#EKYSITB
pqdeploy.envdb[7]=EKYSITA#omzgrid114scan.vzbi.com#1800#EKYSITA
pqdeploy.envdb[8]=EKYSITG#omzgrid114scan.vzbi.com#1800#EKYSITG
pqdeploy.envdb[9]=DITA#ekyfddd1scan.ebiz.verizon.com#1800#PQSITG
 
 

#http://www.ekyfddd1scan.ebiz.verizon.com:1800



Model – Package classes 
	 This package contains all model classes which are used by collector package classes
	Environment.java
	PQDeployApplication.java
	PQDeployCollector.java
	PQDeployEnvResCompData.java
Repository – Package classes 
This package contains DB Specific classes
PQDeployApplicationRepository.java
PQDeployCollectorRepository.java

After running collector, data is stored in DB as below
 
 

 



V.	PROQUEST MQ COLLECTOR
API

PqMqController.java
All controller specific logic is configured here.


 
PQMqStatusRequest.java
All Request Details will be stored here.
 

PQMqStatusService.java
HTTP Response logic is implemented here
   

Repositories:
This repository is an interface defined to access the data. Spring Data repositories usually extend from the Repository or Crud Repository interfaces. If you are using auto-configuration, repositories will be searched from the package containing your main configuration class.
   

4.	PROQUEST-MQ-COLLECTOR 
Root folder is proquest-mq-collector/src/main/java/com/capitalone/dashboard

Collector – Package classes 
This package contains all collector specific implementations

7.	PQMQCollectorTask.java
 	This the core class in this collector. On Starting collector collect() method will execute.
It contains method calls which performs Collector Specific implementation’s 

8.	DefaultPQMQClient.java

This class contains collector specific implementation methods. 
List of methods:
getApplications(String instanceUrl)
	To get Applications details
getEnvironments(PQMQApplication application)
	To get Environment details
getApplicationSettings(Environment env, ObjectId collectorId)
	To get Applications Settings details

9.	PQMQSettings.java
We will declare all configuration details in application.properties . this class is used to read 
those details 
application.properties (Sample)

#Database Name 
dbname=dashboarddb

#Database HostName - default is localhost
#dbhost=localhost

#Database Port - default is 27017
#dbport=9999

#Database Username - default is blank
#dbusername=db

#Database Password - default is blank
#dbpassword=dbpass


#Collector schedule (required)
pqmq.cron=0 0/1 * * * *

#UDeploy server (required) - Can provide multiple
pqmq.mqapps[0]=SOA
pqmq.mqapps[1]=EIB
#Queue manager and HostName/Port specified in formt mqapp#queuemanager#host#ip
pqmq.queuemanager[0]=SOA#SOA1D#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[1]=SOA#SOA2D#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[2]=SOA#SOA3D#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[3]=SOA#SOA4D#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[4]=SOA#SOA1S#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[5]=SOA#SOA2S#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[6]=SOA#SOA3S#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN
pqmq.queuemanager[7]=SOA#SOA4S#soafrdt42.ebiz.verizon.com#4055#SOA.UNO.SVRCONN
pqmq.queuemanager[8]=SOA#SOA1P#soafrdt42.ebiz.verizon.com#3055#SOA.UNO.SVRCONN

pqmq.queuemanager[9]=EIB#EIBDITA#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[10]=EIB#EIBDITB#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[11]=EIB#EIBDITC#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[12]=EIB#EIBDITD#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[13]=EIB#EIBSITA#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[14]=EIB#EIBSITB#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[15]=EIB#EIBSITC#eibsit.verizon.com#2413#EIB.UNO.SVRCONN
pqmq.queuemanager[16]=EIB#EIBSITD#eibsit.verizon.com#2414#EIB.UNO.SVRCONN
pqmq.queuemanager[17]=EIB#EIBPRD1#eibsit.verizon.com#2413#EIB.UNO.SVRCONN

pqmq.filter=*uno* 

Model – Package classes 
	 This package contains all model classes which are used by collector package classes
Environment.java
PQMQApplication.java
PQMQCollector.java
PQMQEnvResCompData.java
Repository – Package classes 
This package contains DB Specific classes
PQMQApplicationRepository.java
PQMQCollectorRepository.java
After running collector, data is stored in DB as below


 


CODEMAAT

svn log http://ekyomta1.vzbi.com:8001/svn/uno/trunk/ -r  {2016-01-01}:{2016-03-15} --xml > jan.xml
svn log http://ekyomta1.vzbi.com:8001/svn/uno/trunk/ -r  {2016-01-15}:{2016-05-31} --xml > march.xml
svn log http://ekyomta1.vzbi.com:8001/svn/uno/trunk/ --xml > complete.xml
ERRORS AND SOLUTIONS
1.com.mongodb.MongoSecurityException: Exception authenticating MongoCredential{mechanism=SCRAM-SHA-1, userName='dashboarduser', source='dashboarddb', password=<hidden>, mechanismProperties={}} 
Caused by: com.mongodb.MongoCommandException: Command failed with error 59: 'no such cmd: saslStart' on server localhost:27017. The full response is { "ok" : 0.0, "errmsg" : "no such c

Solutions
1.	 check  in api\src\main\resources

# Default server configuration values
dbname=dashboard
#dbusername=dashboarduser
#dbpassword=1qazxSw2
dbhost=127.0.0.1
dbport=11500
server.contextPath=/api
server.port=8080


2.	Check Dashboard. Properties
 


3.	Make sure that you created dashboarduser
use dashboarddb
db.createUser(
        {
          user: "dashboarduser",
          pwd: "1qazxSw2",
          roles: [
             {role: "readWrite", db: "dashboarddb"}
                  ]
          })
4.	Check MongoConfig file VS dashboard.properties

    @Value("${dbname:dashboarddb}")
    private String databaseName;
    @Value("${dbhost:localhost}")
    private String host;
    @Value("${dbport:27017}")
    private int port;
    @Value("${dbusername:}")
    private String userName;
    @Value("${dbpassword:}")
    private String password;


2.	com.mongodb.MongoSocketOpenException: Exception opening socket
Open MongoDB connection by running
cd D:\mongodb\bin
d:  
mongod.exe --config="D:\mongodb\mongo.config".


3.	UI- Error: Cannot find where you keep your Bower packages.
Just create the folder bower_components on the same level as node_modules.
 


4.	org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'codeMaatCollectorTask': Invocation of init method failed; nested exception is java.lang.NullPointerException
Check application.properties , the keyword term like Jenkins. Is same in properties file and java files are same or not


