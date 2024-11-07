CI-CD: Jenkins 

CLASS -1 INTRO JENKINS

so far we discussed sQ, maven, maven, tomcat and nexus.
instead of manuvally doing this and create  job, we can integrate this tools with jenkins and run job for CI.

we can integrate all this tools and automate this with CI tools.



popular CI tool jenkins.

free style
maven project
plugins

jenkins security

create cicd using pipeline project.
A. scripted way {groovy}
B. Declarative way

multibranch pipeline
backup
migration
master slave 
jenkins implementation for node js project
J-shared Library.

what is jenkins:
Jenkins, is an open source java based  Continuous Integration, cross-platform tool written in Java. 

Continuous Integration:
===========================
Continuous Integration (CI) is the process of 
automating the build and testing of code every time when  a team member commits changes to version control. 



continuous integrations tools:
maven, SQ, nexus, and tomcat.

CI – Benefits
•	Immediate bug detection
•	No integration step in the Software Development lifecycle
•	A deployable system at any given point> package is already there just to deploy the package to app server.
•	Record of evolution of the project {means it is going to build no going to add it will maintain all history}

bill may failue, if dependencies not correct, or testing not done proper, SQ not running , and this may lead to bill failure.

Continuous Delivery: Continuous Delivery in Jenkins is a software development practice where code changes are automatically built, tested, and deployed to production or staging environments
Sample projects: usually use for external projects: ex: facebook , twitter
before going to deploy we need client signoff conformation to deploy on production.
incontinuous delivery manually we are going to deploy to the production.


code done>>unit test done> integrate>acceptence test> manual push to deploy production.----for this we need client approve for this.

Continuous Deployment: The practicing of automatically deploying every successful build directly into production without any manual steps knows as Continuous deployment.
Sample projects: internal projects. Ex: hrms about employe details.


$$
What Jenkins can do?
$$

•	Integrate with many different Version Control Systems (GitHub, CVS, SVN, TFS …)
•	Generate test reports (JUnit)…  
•	Push the builds to various artifact repositories. Ex: Nexus,  
•	Deploys direc•	Notify stakeholders of build status (Through Email), weather build fail or success.
tly to production or test environments {CI or CD}


 jacoco> through this we can prevent deploy untill it match standar code quality.

 Benefits of Jenkins
✓	Its an open source tool with great community support.
✓	Easy to install and It has a simple configuration through a web-based GUI, which speeds up the Job

if anything error we found we can raise jira ticket to jenkins team to solve this issue. its a free service. support also great support.
https://www.jenkins.io/doc/book/troubleshooting/diagnosing-errors/
✓	It has around 1800+ plugins to ease your work. If a plugin does not exist, just code it up and share with the community (https://plugins.jenkins.io/). plug in is nothing but a piece of SW to enhance the SW. or adding new feature to the SW.
or additional features.

✓	Its built with Java and hence, it is portable on all major platforms.
✓	Good documentation and enriched support articles/information available on internet which will help beginners to start easy.

✓	Specifically, for a test only project, it is used to schedule jobs for regression testing without manual intervention and hence monitor the infrastructural and functional health of an application.
It can be used like a scheduler for integration testing and also can be used to validate new deployments/environments on a single click on a Build now button.

cloudbee jenkins is a enterprice editions and we can expect immediate support.


=========
class-2
=========

we have to SQ, MAven, nexus tomcat has to up and run. before starting the jenkins job.


while creating and after creTE JOB WE have below mentioned components:


1. general 
2. source code management
3. build triggers
4. buils env
5. build  >>. just we need to mention goal names like clean package, clean build, like this.
6. post-build actions.

if we want to update existing configuration we need to check on config tab.


by default it is going to take from master branch




we can configure n no of maven  in jenkins. from global tool config 
also we can specify the versions as er requirement.
and then we can append to the suitable version in build tab before excuting the build now.


after build now, then can check the console out put for default path of jenkins where the code got kept.

/var/lib/jenkins/workspace/myfirst-dev/target/01-maven-web-app.war

after package we need to excute SQ report.

sonar:sonar

so update sonarqube details in pom.xml file in the project directory.

we can give sonarqube url with token in pom .xml of project directory.

then check in sonarqube dash board for any bugs, code smells or vulnerabulities.

once code quLITY DONE,
THEN UPLOAD in artifactory repository.

goto pom.xml in project code and give artifactory urls. like release and snapshot repository details.
then we have to configure credentials in settings.xml in conf directory.

in jenkins home directory, in cli. tools directory.

NOTE: any software installed in jenkins that will go to the tools directory.

/var/lib/jenkins/tools



/var/lib/jenkins/tools/
sample software: hudson.tasks.Maven_MavenInstallation/maven_3.9.6 

in above path we have multiple maven softwares.

if we use first time then software versions related sw will get downloaded.


in maven goto conf/settings.xml>servers tag we are going to cfredentials.

nexus credentials in server tag.


then update goal {clean package sonar:sonar deploy}.

then it will shown what is the new update in build.

then ckeck in nexus dash board. weather new artifact uploded or not.


then deploy application into the tomcat server.


take tomcat server url.

now take plugin called {deploy to war/ear to container}.
with out this plugin we cant deploy app in tomcat.


goto manage jenkins>plugin manager> to install any plug ins;

then goto post-build actions:

give path like 

**/target/app.war

in 
add centainer tab we can deploy our application
select version> tomcat url> tomcat credentials>user/pass> description details we need to mention.

then build now.
update credentials in /opt/user/xmlfile> give roles as manager-gui, admin-gui and manager-script .

before we are following this above type of devops flow...................

how to automate the build trigger process.
=========================================
aS SOON as developer push the code it has to trigger the job
we can use 3 ways: under build triggers:

1. poolSCm > here it will ask schedule time ***** means every minute. here what ever time interval we mentioned as per that jenkins will go and check any updated code or not. based on the commit ID.
if its find any updated code and new commit id. if no updated code and commit id same in jenkins and git then no job trigger will happen.

ex: change project code in GH and see the job trigger in jenkins.

NOTE: if changes are there then only jenkins job will trigger.
started by scm change
2. build periodicall>>>  * * * * * 
start with space, build will trigger every one minute.
it will show started by timer .
NOTE: even though there is no update or change in the code this will get trigger by jenkins.

3. github web hook>>> 

instead of jenking going everytime and checking the updated or change  code its using more server resource.

instead of that 

once developer push the code to SCM git hub will intimate to jenkins abt the change in code or update in the code using git web hook option for this option git hub need admin access. 

jekins side also we need some changes in build triggers> git hub web hook.
take the jenkins url

goto  git hub > goto project ceode settings> and webhooks> 

when ever specific changes happen webhook will intimate post request to jenkins.

along with jenkins url /webhook/ need to update in git hub.

then content type: application/json

select evet tupe: like pull, push, 

only developer push code then only job should trigger.


after change go and check jenkins job will get build and bill number will get generate.
it will show started by git hub push by developer.

ata a time be default 2 build jenkins will run.

if wewant to increase or decrease as per requirement.

build executor status> goto configure> then increase build executor as per our wish.

webhook is the best practice for build trigger.


General:::
enable project based security.
discard old builds
github project
this project is parameterized
throttle builds
execute concurrent builds

 Source Code Management :

 git rpo
 git credentials
 branches

 Build Triggers

Trigger builds remotely (e.g., from scripts)

Build after other projects are built

Build periodically>> as per schedule it will trigger, irespective of change.

GitHub hook trigger for GITScm polling

Poll SCM >>>if any change happence in scm then this will excuete.


Build Environment:::

Delete workspace before build starts
Use secret text(s) or file(s)

Add timestamps to the Console Output
Inspect build log for published build scans
Terminate a build if it's stuck
With Ant

 Build Steps 

 install maven in invoke top-level maven targets



  Post-build Actions 

 Deploy war/ear to a container 
 install and config tomcat server details.


==================
CLASS-3

===============

if we have 100 of builds as a result utilization will be more.

so we have to remove old builds. just 5 build s is fine then we need to do.

Delete workspace before build starts 
---------------------------------------
also time stamp not added to the build whne it excuted and add time stamps to the console.


to prevent this :
goto build environment:
Add timestamps to the Console 
----------------------------------
add timestamp {to add time stamp to the console putput}

Delete workspace before build starts 
-----------------------------------
delete workspace before build starts. {to delete old builds to prevent hadrware utilization}

goto general tab:

discardold build or last 5 builds.
mention in max no builds to keep.

Build Disable 
-----------
-----
if servers are up and runnig due to system maintainance.



in such cases our jobs trigger may not happen and build trigger not done.

for thta we can use one option > {{disable project}}

again we can {{anable}} 

in configure>general >disable project select.





A. jacoco>>> we can use this we can generate junit test cases , if this code ceverage not met upto the standard this will prevent or stop deployment.

to install > manage jenks>manage plugins>available plugs>jacoco

to enable this plug in 

goto> configure>under post build actions> record jacoco coverage report.

here we can mention what % we can expect the code coverage.
if its not met the mention % it eill not going to deploy the application.

if build failed project wont deploy.

check coverage report:

how we can generate the test report for node js projects by using jacoco plugin?


jacoco going to work for the java projects only.

and while build now with jacoco plug-in 
we have to select this check-box.

Build step 'Record JaCoCo coverage report' changed build result to FAILURE

we can create same job which is related to pexist code we can do it wwith the same code . copy option

same job configd we used.


[[[[[[[Jenkins  Directory structure]]]]]]]

/var/lib/jenkins/jobs>>> this directory having 10 directory we are gon g to see in the jobs directory.

what ever jobs we created.

under each directory of job>nextbuild no its a file 
also contains directory called BUILDS


/var/lib/jenkins  >>> jenkins default home directory

here we can see [job] directory inside this jiob 

what ever jobs we created we can see inthis tab /var/lib/jenkins/jobs
>if we go inside of the created directory there will be a builds & config.xml & next build number. 

>again builds having how many times we triggers build and those directories, example if we trigger 3 times a build then 1,2,3 directories will be there.
> if we enter this directory again there will be a log, and changelog and build.xml files.
will be there.

under each job directory we can see next build number.
also it contains one directory called {{{builds}}} how many builds we have done
and each build we have one directories and inthis directory we can find log..or ...console output.
also we have config .xml > and it contains job configurations.like> which are all options and selected option we have done whicle creating the job those things available here.

also we have 
change log.xml > it contains that if we changes anything or updated in github code then those infoavailable inthe change .xml file. for the particular job.

-------------------
work space directory>>>>this contain source code . along with temp directory with jobname.

what ever jobs we created those will create 1 directory.
like job_1, job_1 and temp file of those jobs.

if we want to create many jobs similar to previus job, we can do it with [[[copy from]]] option while creating the job tab.


--------------

tools directory:

============

tools directory contains what ever softwares got installed to global tool configuration here it will store.

--------------------

users: user directory contains user.xml and all the user information available here. each user contains one entry, and if we create one more user then one more tag will be created.
user file will be on xml file format.

----------
{{{{{{{{{PLUG-IN's}}}}}}}}}
---------
this directory having what ever plug-ins we installed those plug ins will be available here.
along with their dependencies.

update directory
----------------

this directory contains what ever updates ready to install those will avialable here.
---------------------
if jenkins server not up and running
then we have to start our service and it not happen
then we have to check from {{{{/var/log/jenkins}}}}> here we have jenkins.log 
 

 job/workspace/tools directories imp.



 ============
&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

Create the Maven Project using Maven Project type 

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
usually > newitem> free style project
instead of this > newitem> maven project>plugin maven integration.

pnce install this plugin maven integration.
we can see maven project option to create JOB.

d/w free style and maven project.

free style: this project we can creat cicd for any programming language not only for java. 

maven project: we can create jobs only for java, which is having maven as a build tool.
main reason for maven project : its mainly or dedicatedly design for java and performance improved. also extra features.


&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

class-4   plug-in management:

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&



plug-in management: which plug-ins we use and purpose ofthose we nedd to explain.

•	Deploy to container>
---------------------------
 The "Deploy to container" plugin in Jenkins facilitates the deployment of artifacts (such as WAR or EAR files) to containerized environments, commonly used for deploying web applications. 

•	Deploy WebLogic>. 
---------------------
 Similar to other deployment plugins in Jenkins, the Deploy WebLogic Plugin automates the deployment process, reducing manual effort and potential errors associated with manual deployments.

•	Maven Integration>>> 
---------------------
to get maven project we can use this plugin, it has extra features 
•	Safe Restart
---------------- 
>>>Jenkins url/restart and safeRestart  >>> restart forcablely stop, safeRestart once all jos running then it will get restart.
•	Advanced plugin in plugin manager>>: to download plugin from external sources.which are not available in jenkins . after install external 0luins, we have to restart.
•	Safe restart plugin: 
--------------------------
will restart Jenkins safely.
•	Next Build Number>>> 
----------------------
changing the next build number instead of correct build number.
Reason to change build number?>>>>when ever Jenkins crashed or started build again to any build tool to avoid the conflict of build no we can switch to future build no.
reason: 
•	JACOCO>>>
•	SSH Agent
•	Email Extension>>> to sent email notifications.
•	SonarQube Scanner>>>
we can directly install and config tthe Sq plugin in jenkins.
to install SQ plugin in Jenkins we can use this. We can integrate sonar qube server details in Jenkins.

•	Audit Trail Plugin >>>how to know who trigger or create the job. Like user details. We can track user details.this is keeps a log who performed particular job. 
once we install the plugin audit tail it will going to add section in main config page

manage jenkins>config system>audit tail > log file> give path/ /var/lib/jenkins>audit_log0---10 mb. this log will create up to 10 mb.
log file size>10 mb again it will create another file with 10 mb.
oalso we can give log file count as per requirement like 5 files and 6 files once this count increased, old files or logs automaticall get delete and keep last 5 files count only.

JOB config history: 
---------------------
which user has configure and what is the configuration ddetails we can get with this plug in.
which line has changes or added what ever the modifications we can find it from this plug in.
we can restore the deleted jobs usind this plugin.


•	Schedule Build >>>
we can schedule jobs. ex: i want to trigger the job only one time anytime then we can schedule only one time.

sample:;: only today it has to trigger.

once we install this plug-in we can see the schedule option in the build then we can schedule it.


•	Artifactory Plugin>>>>>
•	Cloud Foundry
•	Blue Ocean>>> dependency plug-in
•	Publish Over SSH>>> if we want to upload a file one Jenkins to another jenkins
•	ThinBackup>>>> imp plugin to take the Jenkins config files backup we can use this plugins.it is having good futures.
•	Build Name Setter>>> instead of 123 … build no, environment name it has to add.
install bhild setter> goto build env> select set build name >give env name then dev-123 then instaed of build 1 or 2 this value will come.


•	Like dev-1, dev-2, we can customize the build name.
•	
•	Convert To Pipeline>>>>if we want to convert maven or free style   projects, to pipeline projects then we can use this catogory of . convert to pipeline.

•	Main use of this plugin is jobs created with freestylr TO pipeline or maven to maven to pileline we will use this.



@@@@@@@@@
class-5 Jenkins Security, views, port change 
@@@@@@@@@

we can change default path for jenkins from /var/lib/jenkins/ to JENKINS/HOME


Port Number Change
Default 8080, we can change it from 8080 to another from
/usr/lib/systemd/system 
After change restart 

Environment="JENKINS_PORT=8080"


----------------

views
---------------
group the relaven jobs under one name to navigate easily.
jenkins having 100s of jobs dificult to navigate so we can customize out jobs using views.

we can creat a group which is relavent to the project and easy to navigate the jobs.

jenkins security
----------------

how we can provide security for jenkins in terms of access and using.

we should add all the user to the  {{project based matrix stratezy}}

job
run
view
scm
build now
creat
delete

this are the job security options we can provide to the users.
we can do acces for particular job for a particular person.
enable project based security in general tab so that we can provide access to the single user to do the  privilege to do the job.


•	Create Users (Default Admin)> manage Jenkins>manage users> user&pass, email
Configure global security: we can provide access privilege to the users.
User.xml file we will keep user info.
Ldap: to create users eithout manually.
Authorization: if we hv valida credentials we ca do administration access also.

Rolebased strstegy: /projectbased authorized strategy, 

•	Provide the specific access Jenkins
•	Provide the access to specific access to specific projects
-----------------------
jenkins backup
----------------------

to take the back up we need to install one plug-in called thinbackup
once installed
goto MJ>tools and actions> thinbackup> we can see
backupnow/restore/settings options.
before takind backup we need to first configure the settings.
1.Backup directory
?Backup schedule for full backups   >>>> everytime it will take the backsp.
Backup schedule for differential backups >>>> what ever update or changes done before backup this backup only it wll take.
?
?Max number of backup sets
?which files we need to take the backup all the detaile should providde to the settings.

we can zip ols backup to zipfile format.
once done the configure detail in settings then click on backup now.
and check in jenkins server. /var/lib/jenkins/jenkinsbackup.

we founs backup files as shown :FULL-2024-03-12_18-18

NOTE: within one minute if we take backups it wont take new backup, once minute cressed then again it will take new nackup after 1 minute.



Backup schedule for full backups>>>>> means everytime it will take backups
Backup schedule for differential backups/>>>>> means what evr the updates or changes are there then on,y it will take backup
 

 project wise we can maintain 50 backups.

below files we can take backups:

Bakup build results

Backup build archive

Backup only builds marked to keep

Backup userContent folder

Backup next build number file

Backup plugins archives

Backup config-history folder

Backup additional files

Files included in backup (regular expression)
Clean up differential backups

Move old backups to ZIP files

Stop the backup as soon as an exception occurs in the file handling

===========
CLASS-6 how to create job using pipeline project type
===========

as pf now we discussed abt frestyle and maven project type of ci.

now pipeline project..


here we are going to write pipe line script. and we can customize our cicd processs.

its very easy to integrate other tools with jenkins.

pipeline script we can write in 2 ways
1. scripted way >>> here pipeline script is going to use that all the groovy sysntax.

ex:

by default it is going to run in master instance or master node.
if we specify or dont specify it will run on master node.

cicd process first stype: getting the code from scm. {github}
if we want to get the code each task we are going to write one stage.

node {

stage ('checkout code'){
git branch: 'development', credentialsId: '8e9db6b7-9087-4522-94ea-ccfb864d2e47', url: 'https://github.com/12072016/maven-web-application.git'
}

stage ('BUILD') {
sh "$mavenHome/bin/mvn clean package"   

}

}//node closing



/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3.9.4
NOTE: def we can use to install any package

def mavenHome = tool name: "maven3.8.4"

newitem>pipelinescriptedway>select pipeline>ok
then goto  pipeline script> pipeline syntax
there we can see snippet generator>sample step select git>give repository url>branch name
give credentials >clicl on generate script.

copy and paste script. it into  checkout stage 


stage2:

we need to do the build.

maven installed in jenkins so take maven inputls like version and update in variables.

stage3:
 SonarQube report generation.
 update sonar url and credentials in pom.xml file in project directory.
with same branch.

stage ('SonarQubeReport'){

sh "$mavenHome/bin/mvn sonar:sonar" 
    
}

stage:4

upload artifacts into the nexus repository.

stage ('Upload artifacts into nexus server'){
 sh "$mavenHome/bin/mvn deploy"  
    
}

stage:5
deploy application into tomcat server.
stage('deploy app into tomcat '){


}


here scripted way wwe can write groovy script like above or, if any project source code having jenkinsfile we can copy url, credentials and branch details and we can excute the build.

for this we can select pipeline script from scm option.
else 
pipeline script. to write groovy script.

Global Variable Reference
****************************
smaples
echo "the node name is :" ${env.NODE_NAME}
echo "the job name is :" ${env.JOB_NAME}
echo "the build number is :" ${env.BUILD_NUMBER}

like this many global env we can refere from reference and add t to the groovy script

so that dynamically we can get the values.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
CLASS-7 declarative way.

************************
scripted way we will use
node{

}

declaratrive way>>>

pipeline {
agent any//it is going to run by defaukt in master node.

//if we wan to specify some other node.

tools{
maven "maven3.8.4"
}

agent{
label 'nodename'
}

stages{
    //get the code from github repo
  stage('checkoutCode'){
    steps{
   git branch: 'development', credentialsId: '8e9db6b7-9087-4522-94ea-ccfb864d2e47', url: 'https://github.com/12072016/maven-web-application.git'
    }
  }
   //Do the build
stages{
  steps{
    sh "mvn clean package"
  }
}

//execute sonarqube report
stage('sonarqubereport'){
steps{
    sh "mvn sonar:sonar"
}

}

//upload artifacts into nexus
stage('upload artifacts into artifact repository'){
steps{
    sh "mvn deploy"
}
}

//deploy app into tomcat
stage('deploy app into tomcat'){
steps{
    ssh agent
}
}
}//stages closing

}//pipeline closing 



NOTE: as like scripted way pipeline codesnippet is there similarly
in declarative way also we have declarative direct generate option here we have AGENT,TOOLS, STAGES,triggers,  MANY MORE.
FOR PROPERTIES OF A JOB CREATION LIKE DISCARD OLD BUILDS, TIME STAMPS ALL OTHER OPTIONS ARE THERE.

=====================
MAster-slave architecture  class -8
========================

build with parameters>>> if we want to pass parameters with dynamically we will use this build with parameters.




we can build with parameters:
example:
facebook-dev ==developement branch
facebook-QA ===stage branch
facebook-prod ===master branch


there are 3 jobs .
creating 3 jobs for a same project we can creat 1 job and we can pass values dynamically.


example:
newitem>free sytele project>git url & credentials>here branch no need to mentios {{instead of this this project is parametarized in general tab}}

>branch name> development>master>uat>QA mention branch names like this.


in source code management branch name mentioned like this.
*/${branchName}

select string parameter in general name>default value

under build step:
excute shell

echo"the person name is ......"
then click on buildwith parameters.

by default it will take devel


opment as a default branch as, we mentioned dev-master-uat-and QA .

this is free or maven we can get like this.
if its pipeline then.......

with parabuild we can do both maven and freestyle. aswell pipeline script.


master-slave architecture:

purpose of the M-S architecture. is to improve the performance.

if we have 100 jobs and if we trigger all the jobs in master instance it may take time.
instead if we distribute some jobs to slave nodes the load we can manage.

for slave nodes we nned to install java.

all the jobs information available in mster node only.

dependes on the surver resources we can assign more jobs.

/var/lid/jenkins/job.

slave creation::
================
!after instance creation need to install java in slave node.
!create one directory for slave jobs 
!togo jenkins gui>goto manage jenks>manage nodes and clouds> we can see how many nodes are there> new node> slave name>desc> no of excutors how many jobs run parlelly>remote root directory>slave path> label name>
master -slave protocal TCP and connection tyoe is ssh .

host details>credentials>private key copy paste in this private key field> availability {{means when slave need to work 1. when its required or if load more. 2. as per schedule timing 3. always avail as much as possible }}

check log> ur slave is ready to run the job. so connection established to master node.


how to configure to run this job in slave>>>>

goto any project click on config >under general >restrict where thi job can be run>give slave naame in the box .....

if master instance is down slave will work.

what ever we configure inthe global tool those tools can be applied to the slave nodes aswell.

jenkins multibranch pipeline: pending
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
we have 50 branches we want to implement continuous integration.

inthis case we can use multibranch pipeline.

if we wan to implement CI for this project then we can go with multibranch pipeline.

for this method.
A. if we use this MB-pipeline
we will use repository URl
and check what are the branches are there and script filename 
we are going to specify script filename.

what ever the script name we specify tht branch it will find and create the job automatically with that branch.

if we want to create multibranch pipeline., project code should have pipeline script or not?

with out pipeline script it will wont work, we should have pipeline script.

freestyle and maven projects we no need pipeline script.


once we given repo url, and script file name it will search the file name in all the branches and it create the job which branches having this file name.

if filename not matches then it will show as below in Scan Repository Log
  ‘Jenkinsfile’ not found
    Does not meet criteria

if filename  matches then it will show as below in Scan Repository Log
 Getting remote pull requests...
      ‘Jenkinsfile’ found
    Met criteria
Scheduled build for branch: development


we can enable the periodically option and if any update then it will trigger the job .......

==================
class-9 JENKINS CLI
=============

use of jenkins cli and why we need ?
creating jobs, create view, triggering jobs, we can perform through scripts.

we can automate manual tasks. through jenkin cli. and also performance also good.

we can automate the regular jobs.

we have to download one jar file.
just we can add cli to jenkins url.

access with username and password like below to access 


we can get the list of jobs with this commands
java -jar jenkins-cli.jar -auth srishil:nandan -s http://3.92.184.198:8080/ list-jobs


how to create jenkns automate script.

example: if we wan tto crea a build then goto build option , once click on this job we can see the scripted like below:

java -jar jenkins-cli.jar -s http://3.92.184.198:8080/ build JOB 

copy this to the any script file like build.sh and keep it in the file

java -jar jenkins-cli.jar -auth srishil:nandan -s http://3.92.184.198:8080/ build test1
echo "Build the job"
echo "----------------------"
the excute the file sh build.sh ----output will come like below.

then build will trigger with given name, goto jenkins dashboard and check weather job triggred or not.



Jenkins Migration :

currently jenkins hosted in AWS, this jenkins hsaving 100 jobs.
aws charging more , so we migrated to azure,
if we wanto migrate it to azure.

install same jenkins version in auzre..

rename the home directory aws /var/lib/jenkins to 
azure
/var/lib/jenkins_backup

stop jenkins and copy directory from aws to azure. also some config files
then start jenkins servers.
else do it through  plug-in called job-import
this plug in has to install in azure then we are going to get user/password and url thrn login to this then move all the config and files .




===========
CLASS-10 CICD for NODE JS
===================

many application developing with node js.

newitem,>nodejstages cicd>pipeline>
script pipeline

node {
stage('checkout code'){
    git credentialsId: '8e9db6b7-9087-4522-94ea-ccfb864d2e47', url: 'https://github.com/12072016/nodejs-app-mss.git'
    }


stage ('build) {
sh "npm install"

}

stage ('executesonarqube report'){
nodejs(nodeJSinstallationName: ')


}



}//node closing


install noejs plug in


nexus crend in settings.xml      in node js .npmrc file
maven java project               nodejs code
mvn deploy                        npm publish
mvn clean package                 npm install
mvn sonar:sonar                   npm run sonar
pom.xml                           package.json > we have dependencies and modules

dependencies check in local repo      here all the deendencies going to creat node_module 

what evr the software we are going to instal through global toll config all the softwares are avail in tools directory.


=============

shared libraries:
=============
Jenkins Shared library is the concept of having a common pipeline code in the version control system that can be used by any number of pipelines just by referencing it. In fact, multiple teams can use the same library for their pipelines. 

if we want to share source code or pipeline script to other projects we will use this share libraries.


its kind of reusing the existing code.

here we have 2 steps:

A. vars: This directory holds all the global shared library code that can be called from a pipeline. It has all the library files with a .groovy extension. 

keep  share libraries repo to the source code repository.

B. add git hub shared library to jenkins:

goto manage jenkins and configure systems.

search with global pipeline libraryes.

name: any name for library
deffault version >main or master
modern scm>git hub url and paste to project repository field.

000000000000000000
Class-11
000000000000000000

Upstream& Downstream

facebook-dev-----upstream job for qa
facebook-qa------downstream job for dev and upstream job for prod
facebook-prod----downstream job for qa, 

after done new item and job cretae, goto 
BUILD triggers> then 
Build after other projects are built



with this features we can create 3 jobs 

simuntaniously....instead of manual trigger
we can trigger all jobs one by one with this feature.

-----------------



=================================================
JENKINS INTERVIEW 
QUESTIONS

1. What is Jenkins
Ans) Jenkins is an open-source automation server. Jenkins is a continuous integration tool 
developed in Java. Jenkins helps to automate the non-human part of software development 
process, with continuous integration and facilitating technical aspects of continuous delivery.


2. What is the difference between Jenkins and Hudson
Ans) Jenkins is the new Hudson. It really is more like a rename, not a fork, 
since the whole development community moved to Jenkins. (Oracle is 
left sitting in a corner holding their old ball Hudson, but it’s just a soul-less project now.).
In a nutshell Jenkins CI is the leading open-source continuous integration server.

3. What SCM tools does Jenkins support?
Ans) Microsoft Team Foundation Server (TFS), GitHub, big backet, Azure DevOps, Concurrent Versions System {CVS}
4. How can you tell what version of Jenkins you are using?
Ans) in dash board we can find it
5. What is continuous integration in Jenkins?
Ans) Continuous integration is a process in which all development work is integrated as early as 
possible. The resulting artifacts are automatically created and tested. This process allows to 
identify errors as early as possible. Jenkins is a popular open source tool to perform continuous 
integration and build automation.

6. What are the pre-requisites for using Jenkins
Ans) Java Runtime Environment (JRE) or Java Development Kit (JDK), OS, HardwaRE, Network Accessibility, web broser, Permissions, ports, 

7. How can you move or copy Jenkins from one server to another server
Ans) Moving or copying Jenkins from one server to another server involves several steps to ensure that all configurations, plugins, jobs, and data are transferred correctly. Here's a general outline of the process:

Backup Jenkins Data:

Before you begin, it's crucial to back up your Jenkins data, including configurations, job configurations, build histories, and any other important data. You can use the Jenkins Backup Plugin or manually backup the Jenkins home directory.
Install Jenkins on the New Server:

Install Jenkins on the new server by downloading and setting up the Jenkins WAR file or using a package manager depending on your operating system. Follow the installation instructions provided on the Jenkins website.
Stop Jenkins on Both Servers:

Stop Jenkins service on both the old and new servers to prevent any data corruption during the transfer process.
Copy Jenkins Home Directory:

Copy the entire Jenkins home directory from the old server to the new server. This directory typically contains all Jenkins configurations, jobs, plugins, and other data.
Ensure that the file permissions and ownerships are preserved during the copy process.

Start Jenkins on the New Server:

Once the files are copied and configurations are adjusted, start Jenkins on the new server.
Monitor the Jenkins logs for any errors during startup to ensure everything is functioning correctly.
Verify Jenkins Configuration:

Access the Jenkins web interface on the new server and verify that all configurations, jobs, and plugins have been successfully migrated.
Test running a few jobs to ensure that Jenkins is functioning as expected on the new server.

Monitor for Issues:

Monitor the Jenkins instance on the new server for any issues or unexpected behavior, especially during the initial transition period.


8. Commands to use to start Jenkins manually
Ans) systemctl enable &start jenkins
9. What are the most useful plugins in Jenkins
Ans) 
10. How to create a Jenkins job and what are the types
Ans) Access Jenkins Dashboard>Log in>New Item>Enter Job Name>Select Job Type> 

then : Freestyle project >>>
The purpose of a freestyle project in Jenkins is to allow users to {{{create and configure custom build jobs with flexible options}}}, enabling them to execute various tasks such as building, testing, and deploying software in a straightforward manner without strict guidelines or predefined structures.

Maven project
Build a maven project. Jenkins takes advantage of your POM files and drastically reduces the configuration.

Pipeline

The purpose of a pipeline in Jenkins is to create a structured, scriptable workflow for building, testing, and deploying software, allowing for better automation, version control, and visualization of the entire software delivery process.

Multi-configuration project
Suitable for projects that need a large number of different configurations, such as testing on multiple environments, platform-specific builds, etc.

Multibranch Pipeline
Creates a set of Pipeline projects according to detected branches in one SCM repository.
with scripted file having with multiple branches and those jobs will run according to the scriptedfile haveing brances.

Copy from
If you want to create a new item from other existing, you can use this option:

11. What are the two components that Jenkins mainly integrate with?
Ans) Version Control Systems (VCS):
Jenkins integrates closely with various version control systems such as Git, Subversion (SVN), Mercurial, CVS, 

whenever there's a new commit or a specific event occurs (e.g., pull requests, branch creations).

Build Tools and Automation Scripts:
Jenkins can integrate with a wide range of build tools and automation scripts used in the software development process. These tools include Apache Maven, Gradle, Ant, Shell scripts, Windows batch commands, Docker, Kubernetes, and many others. Integration with build tools allows Jenkins to execute build tasks, run tests, package applications, and perform other automated tasks as part of the CI/CD pipeline.


12. What is the default session timeout value in Jenkins and How can you increase the 
session timeout value?
Ans) 
In Jenkins, the default session timeout value is typically set to 30 minute

Access Jenkins Dashboard>click on the "Manage Jenkins" >Configure Global Security">Access Control" section, where you'll find the "Session Timeout" configuration option. By default, it's set to 30 minutes. specifying the duration in minutes.

Save Configuration Changes

13. Explain about Jenkins security mechanism

Ans) Authentication: Jenkins supports various authentication methods such as LDAP, Active Directory, Unix user/group database, and its own internal user database. Users must authenticate themselves before accessing Jenkins.

Authorization: Jenkins offers fine-grained authorization controls to specify what actions users or groups can perform. Authorization can be based on user roles, project roles, or matrix-based access control.

Project-based Matrix Authorization Strategy: This security strategy allows administrators to define permissions for specific projects or jobs based on user roles or groups.

Global Matrix Authorization Strategy: Admins can configure global permissions using a matrix-based approach, defining what actions each user or group can perform across the entire Jenkins instance.

Role-Based Access Control (RBAC): Jenkins supports RBAC, allowing administrators to define roles with specific permissions and assign users or groups to these roles.

Security Realms: Jenkins allows integration with external authentication systems such as LDAP or Active Directory through security realms, enabling single sign-on (SSO) capabilities.

CSRF Protection: Jenkins includes Cross-Site Request Forgery (CSRF) protection mechanisms to prevent unauthorized actions initiated by malicious websites.

Session Management: Jenkins offers session management features, including session timeout settings and session fixation protection, to enhance security.



14. How can you pass parameters from one job to another job in Jenkins?
Ans) In Jenkins, you can pass parameters from one job to another job using the "Parameterized Trigger" feature:

Configure the upstream job to trigger the downstream job.
Define parameters in the upstream job.
Configure the downstream job to accept parameters.
Pass the parameters from the upstream job to the downstream job when triggering it.
This allows for seamless communication between jobs and facilitates building dynamic and flexible pipelines.


15. Explain about build pipeline in Jenkins?
Ans) 
In Jenkins, a build pipeline represents the workflow of a software project, from code commit to deployment. It visualizes the stages and transitions through which code progresses, typically including stages like build, test, and deploy. Each stage consists of one or more jobs that execute specific tasks, and the pipeline provides a clear overview of the project's progress and status. Build pipelines help streamline the development process, automate tasks, and ensure consistent and reliable software delivery.


16. How can someone execute the jobs in Jenkins without having permissions to execute the 
job?
Ans) In Jenkins, if someone doesn't have permissions to execute a job directly, they can still trigger the job indirectly through other means, such as:

Using Parameterized Builds: If the job is configured with parameters, anyone with permission to build the job indirectly can trigger it by providing the required parameters.

Using Upstream Jobs: If the job is part of a larger pipeline or chain of jobs, someone with permission to trigger the upstream job can indirectly trigger the downstream job as part of the pipeline.

Using Automated Triggers: Jobs can be triggered automatically based on events such as code commits, time schedules, or external triggers like webhook notifications. Even if someone doesn't have direct permission to trigger the job, if the trigger condition is met, the job will be executed automatically.

Using Build Pipelines: If the job is part of a build pipeline, someone with permission to trigger the pipeline can indirectly trigger the job as part of the pipeline's execution flow.


17. How to re-execute a parameterized build job without entering the parameter values 
when the job fails? 

Install the Rebuild Plugin:

If the Rebuild Plugin is not already installed on your Jenkins instance, you'll need to install it. You can install it via the Jenkins Plugin Manager.

Note:- Job should not ask for parameters and it should run with the values of parameters 
that you entered during previous execution

18. How to install plugins in Jenkins?
Ans) Manage Jenkins>Access Plugin Manager>Choose Plugin Installation Method> Available>Installed>Select Plugins for Installation:>lick Install/Download:>verify installation.



20. How to run jobs in slaves?
Ans) To create and configure slaves (or nodes) in Jenkins, follow these steps:

Access Jenkins Dashboard: Log in to your Jenkins instance and access the dashboard.

Navigate to Manage Jenkins: Click on "Manage Jenkins" on the left sidebar.

Access Manage Nodes: Within the "Manage Jenkins" page, select "Manage Nodes and Clouds."

Click on "New Node": On the "Nodes" page, click on the "New Node" or "New Node/Slave" button, depending on your Jenkins version.

Enter Node Configuration:

Enter a name for the node in the "Node name" field.
Choose the "Permanent Agent" option.
Click "OK" or "Save" to proceed.
Configure Node Details:

Fill in the required fields such as the number of executors, remote root directory, labels, and launch method.
For a basic setup, you may specify the remote root directory and the number of executors (build slots) for the node.
Choose the launch method depending on how you want to start the slave agent:
Launch agent via Java Web Start: Suitable for agents running on the same network as the Jenkins master.
Launch agent via execution of command on master: Suitable for agents running on remote machines accessed via SSH.
Launch agent via executable for agents running ontion of command on agent: Sui the same machine as the Jenkins master.
Save Node Configuration: Click "Save" to save the node configuration.

Connect Slave to Jenkins Master:

Follow the instructions provided in the node configuration page to connect the slave to the Jenkins master.
Depending on the launch method chosen, you may need to download the agent JAR file or execute a command on the slave machine.
Verify Connection: Once the slave is connected to the master, it should appear in the list of nodes on the "Nodes" page with an online status.

(Optional) Configure Labels: Assign labels to the nodes to categorize them based on their capabilities or roles.




22) What is Maven and what is Jenkins?
Ans) Maven is a build tool, in short a successor of ant. It helps in build and version control. 
However, Jenkins is continuous integration system, where in maven is used for build. Jenkins 
can be used to automate the deployment process.

Why do we use Jenkins?
Ans) Jenkins is an open-source continuous integration software tool written in the Java 
programming language for testing and reporting on isolated changes in a larger code base in real 
time. The Jenkins software enables developers to find and solve defects in a code base rapidly 
and to automate testing of their builds.


What plugins have you used in Jenkins?
Ans) 
 
Explain CI/CD and how have you implemented it in Jenkins
Ans) 
 CI/CD (Continuous Integration/Continuous Delivery) is a software development practice that involves automating the process of integrating code changes into a shared repository, building and testing the code, and delivering the changes to production in a rapid and reliable manner.

In Jenkins, CI/CD is implemented by setting up pipelines that automate the entire software delivery process, from code commit to deployment. This typically involves:

Continuous Integration (CI):
--------------------------------
Automatically trigger builds whenever code changes are pushed to the repository.
Compile code, run automated tests, and generate artifacts for deployment.
Provide feedback to developers about the quality of their code.

Continuous Delivery (CD):
--------------------------
Automate the deployment process to staging or testing environments after successful CI builds.
Perform additional testing, such as integration or acceptance tests, in the staging environment.
Automatically deploy changes to production once they pass all tests in the staging environment.

In Jenkins, CI/CD is implemented using pipelines, which are defined as code using a Jenkinsfile or through visual pipeline editors. Pipelines consist of stages, each representing a step in the software delivery process, such as build, test, deploy, and so on. Within each stage, Jenkins executes various tasks or jobs defined in the pipeline, such as compiling code, running tests, and deploying applications.

By automating the CI/CD process in Jenkins, teams can release software more frequently, with higher quality and reliability, ultimately improving the speed and efficiency of software delivery.



How did you report build results to users? What ways are you familiar with for reporting 
results?
Ans) 
 Email Notifications: Configure Jenkins to send email notifications to users or distribution lists after each build, providing information about the build status, test results, and any other relevant details.
 Build Results Summary: Jenkins provides a build results summary on the build details page, showing information such as build status, duration, and console output. Users can view this summary directly in the Jenkins interface.

 Webhooks: Configure Jenkins to trigger webhooks to external systems or services, notifying users about build status changes. Users can receive notifications through various channels such as chat, SMS, or custom integrations.


You need to run unit tests every time a change submitted to a given project. Describe in 
details how your pipeline would look like and what will be executed in each stage.
Ans) 
Here's a simple pipeline setup for running unit tests every time a change is submitted to a project:

Checkout Stage: This stage checks out the code from your version control system (e.g., Git).

Unit Test Stage: This stage executes your unit tests.

Notification Stage: This stage notifies relevant parties (e.g., developers, team leads) of the test results.

Each stage can execute a series of commands or scripts. For example:

Checkout Stage: It typically involves using a Git plugin or a command-line tool to pull the latest code from the repository.

Unit Test Stage: This stage runs your unit tests. You might use a testing framework like JUnit for Java, pytest for Python, or Mocha for JavaScript.

Notification Stage: This stage can send notifications via email, chat messages (e.g., Slack), or other collaboration tools. You can use Jenkins plugins or custom scripts for this purpose.

The pipeline can be configured to trigger automatically whenever a change is submitted to the project repository, ensuring that unit tests are run promptly after each code change.


How to secure Jenkins?
Ans) 
 Authentication: Implement strong authentication mechanisms to control access to Jenkins
Authorization: Configure authorization settings to restrict access to specific Jenkins resources based on user roles or groups. Use Jenkins' matrix-based security or role-based access control (RBAC) plugins to define fine-grained permissions.
Secure Jenkins Admin Access: Limit administrative access to Jenkins by restricting who has administrator privileges. Avoid sharing administrator credentials and use strong passwords or SSH keys for admin accounts.
Use Security Plugins: Utilize Jenkins security plugins to enhance security features, such as Role-Based Access Control (RBAC), Two-Factor Authentication (2FA), and Audit Trail Logging.


 
How to acquire multiple nodes for one specific build?
Ans) In Jenkins, you can acquire multiple nodes for one specific build by configuring a Jenkins job to use a multi-configuration project or a matrix project. This allows you to define axes, such as different nodes, and Jenkins will run the build on each combination of the axes.

Here's a simple guide:

Create a new Jenkins job.
Choose "Multi-configuration project" or "Matrix project" as the job type.
Configure the axes to define the different nodes you want to use for the build.
Set up the build steps as usual.
When you trigger the build, Jenkins will run it on each combination of the axes, effectively acquiring multiple nodes for the build.
That's it! You now have multiple nodes for one specific build in Jenkins.

 
Whenever a build fails, you would like to notify the team owning the job regarding the 
failure and provide failure reason. How would you do that?

Ans) To notify the team owning the job regarding a build failure and provide the failure reason in Jenkins, you can use Jenkins' built-in email notification feature along with post-build actions. Here's how you can set it up:

Configure Email Notifications:

Navigate to your Jenkins job's configuration page.
Scroll down to the "Post-build Actions" section.
Click on "Add post-build action" and select "Editable Email Notification."
Configure Email Recipients:

In the "Editable Email Notification" section, configure the recipients of the email notification. You can specify individual email addresses, mailing lists, or use variables to dynamically determine the recipients.

 
There are four teams in your organization. How to prioritize the builds of each team? So 
the jobs of team x will always run before team y for example
If you are managing a dozen of jobs, you can probably use the Jenkins UI. But how do you 
manage the creation and deletion of hundreds of jobs every week/month?
Ans) To manage the prioritization of builds for multiple teams, especially at scale with hundreds of jobs being created and deleted regularly, you can utilize Jenkins along with some automation and scripting. Here's a general approach:

Job Configuration Templates: Create job configuration templates for each team's builds. These templates should include common configurations and settings that are specific to each team's requirements.

Job Creation Automation: Develop scripts or use Jenkins APIs to automate the creation of jobs based on these templates. You can have scripts that generate jobs for each team based on their configurations. This can be done using Jenkins CLI, Jenkins REST API, or Jenkins Job DSL (Domain Specific Language).

Job Deletion Automation: Similarly, develop scripts to automate the deletion of jobs when they are no longer needed. This could be based on certain criteria such as expiration date, inactivity, or specific triggers.

Queue Prioritization: Configure Jenkins to prioritize the build queue based on the teams' priorities. You can achieve this by assigning labels to jobs or using Jenkins plugins like Priority Sorter Plugin to define rules for prioritizing builds.

Dependency Management: If there are dependencies between jobs or teams, ensure that these dependencies are managed properly. For example, if Team X's build depends on Team Y's build, ensure that Team Y's build is triggered first.

Monitoring and Optimization: Regularly monitor the performance of your Jenkins instance and job queues. Optimize the automation scripts and configurations as needed to ensure smooth operation and efficient resource utilization.

Authentication and Access Control: Implement proper authentication and access control mechanisms to ensure that only authorized users can create, modify, or delete jobs.


 
What are some of Jenkins limitations?
Ans) Lack of built-in support for advanced pipeline visualization and monitoring.
Steep learning curve for beginners.
Reliability issues with plugins and dependencies.
Resource-intensive for large-scale deployments.
Limited built-in support for continuous delivery and deployment.
Limited out-of-the-box security features.

 
How would you implement an option of a starting a build from a certain stage and not 
from the beginning?
Ans) Define Pipeline Stages: Structure your Jenkins Pipeline script into multiple stages, each representing a distinct part of your build process.

Use Input Step: Insert an "input" step at strategic points in your Pipeline script where you want to allow users to choose whether to continue from that point or abort. This step pauses the pipeline and waits for user input.

 
Do you have experience with developing a Jenkins plugin? Can you describe this 
experience?
Ans) Choosing Plugin Type: Decide the type of plugin you want to develop. Jenkins supports various types including Pipeline Steps, Builders, Notifiers, SCM, and more.

Writing Plugin Code: Write Java code to implement the functionality of your plugin. This involves creating classes that extend Jenkins extension points, such as Builder, Publisher, or ExtensionPoint.

Testing: Develop unit tests to ensure the correctness of your plugin's functionality. Jenkins provides a testing framework for plugin development.

 
Have you written Jenkins scripts? If yes, what for and how they work?
Ans) Jenkins scripts are typically written in Groovy, which is a scripting language that runs on the Java Virtual Machine (JVM). There are two main types of scripts used in Jenkins:

Pipeline Scripts: Jenkins Pipeline is a powerful way to describe your build pipeline as code. Pipeline scripts define the entire build process, including stages, steps, and conditions, in a Groovy script. These scripts can be written directly in the Jenkins web UI using the Pipeline Syntax or Pipeline script editor, or they can be stored in a Jenkinsfile in your source code repository.

Pipeline scripts allow you to define complex build workflows, including parallel execution, error handling, and integration with external tools and services. They provide a flexible and reusable way to manage your build process as code.

Scripted and Declarative Pipeline: There are two syntaxes for writing Pipeline scripts in Jenkins: Scripted Pipeline and Declarative Pipeline.

Scripted Pipeline: Scripted Pipeline is a Groovy-based DSL that allows for maximum flexibility and control over your build process. You write your Pipeline script using Groovy syntax, with direct access to Jenkins APIs and features.

Declarative Pipeline: Declarative Pipeline is a more structured and opinionated approach to defining your build pipeline. It provides a simpler syntax and a set of predefined steps and directives for common build tasks. Declarative Pipeline is recommended for users who are new to Jenkins Pipeline or who prefer a more declarative style of scripting.



 
In Jenkins, if build fails, how you will troubleshoot?
Ans) Review Console Output: Start by examining the console output of the failed build. Jenkins provides detailed logs of each build step, including any error messages or stack traces. Look for any error messages or warnings that indicate what went wrong.

Check Build Configuration: Verify the configuration of the failed build job in Jenkins. Ensure that all required parameters, settings, and dependencies are correctly configured. Look for any misconfigurations or missing configurations that may have caused the failure.

Inspect SCM Changes: If the failed build is triggered by changes from a source code management (SCM) system such as Git or SVN, review the recent changesets or commits. Check if any recent changes introduced errors or unexpected behavior that could have caused the build failure.

Collaborate and Seek Help: Collaborate with team members, developers, or system administrators to troubleshoot and resolve the build failure. Share relevant information, logs, and findings to get insights and assistance from others.


How to give access to the user to only build now option for a particular job?
Ans) 
To give a user access to only the "Build Now" option for a particular job in Jenkins, you can configure permissions using Jenkins' built-in security features. Here's how you can achieve this:

Install and Configure Jenkins Authorization Plugin: If you haven't already done so, install the Jenkins Authorization Plugin. This plugin allows you to define and manage user permissions within Jenkins.

Create a New Jenkins User: If the user doesn't already exist, create a new user account for them in Jenkins. You can do this by navigating to "Manage Jenkins" > "Manage Users" > "Create User".

Assign Permissions: Navigate to the job for which you want to restrict access to only the "Build Now" option. Then, follow these steps:

a. Click on the job name to access its configuration page.

b. Navigate to "Configure" or "Job-based Security" (depending on your Jenkins version).

c. Look for the section related to permissions or access control. This section may be labeled "Authorization" or "Access Control".

d. Find the option to grant permissions to specific users or groups.

e. Grant the user permission to "Build" the job. This permission should only include the "Build Now" option and exclude other build-related actions such as configuring or deleting the job.

Save Configuration: Once you've assigned the appropriate permissions to the user, save the job configuration.


================================JENKINS BY MAMU=====================
there is no architecture in jenkins---

but we have master-slave {or NODE}---this is optional

usually jenkins are standalone.

if we have 2 types of apps 1.jav2..net

one app test in master and another one in slave.we can use.

else we can distribute jobs in master and slave. its cost.


master and slave is the diferentiate the jobs.

like uat-slave1
qa-slave2
prod-slave3

master have the all info abt slave.
slave not require jenkins. only java requuired. or which app is running on slave.
develepors will chose which language run in slave/

jenkins ---is a ci tool 

pipeline
freestyle> all config are manual

template model job
maven job-----only for java application.
pipeline> in a order everything.

GENEral
============
Enable project-based security----we can enable and disable the projet if not nessary, again we can enable if require.
Discard old builds----to remove old builds we can choose this option like, how many days builds and max builds to keep.

GitHub project-----to provide git url ....which repo we are working.
This project is parameterized----inputs for the job. 
and single jon run for dirfferent projects.

Throttle builds

Execute concurrent builds if necessary-----it will run jobs randomply.

 Source Code Management :
======================
 git url and credentials



Build Triggers
===============
Trigger builds remotely (e.g., from scripts)
?----excute builds in remotely
Build after other projects are built
?
Build periodically
?
Deploy periodically
?
GitHub hook trigger for GITScm polling
? after commit done in git build job
Poll SCM
? run job as per schedule.


Build Environment
=====================
Delete workspace before build starts
Use secret text(s) or file(s)
?
Provide Configuration files
?
Add timestamps to the Console Output
Inspect build log for published build scans
Provide Node & npm bin/ folder to PATH
SSH Agent
Set Build Name
?
Terminate a build if it's stuck
With Ant
?


Build Steps
==============
jenkins using which build app like mavn or gradle 

Post-build Actions
============
after build actions.

like notifications
build status
archive artifacts
delete build when job compleetes.


jenkins template model job: upstream and down stream jobs.

we have 3 jobs 
job1
job2
job3


1st jobs input for 2 job and 2nd job input for 3rd job.
if job 1 fails jo2 wont run and 2nd job failed 3 rd job wont run.



==================in java we have maven project pipeline....to test java


jobs types:
java application maven
free style job
maven plugin install.


pipeline: means we will do it without maNUAL intervention like scriscriptedway this are 2 types.


declarative>>>>>

pipeline{
agent any 
stages{
stage('git checkout') {
steps{
  git credentialsId: '8e9db6b7-9087-4522-94ea-ccfb864d2e47', url: 'https://github.com/classes-101/test-maven.git'

  }
  }
stage('install'){
steps{
sh "mvn install"
  }
  }

  stage('TEST'){
steps{
sh "mvn test"
  }
  }

  stage('compile'){
steps{
sh "mvn compile"
  }
  }

  stage('package'){
steps{
sh "mvn package"
  }
  }
}


}


=========
maven>
git>
excute shell
mavn install
mvn test
mvn compile
mvn package
=====================

scripted way.>>>>through scripts we will use the scripted way.


node{
stage('scm'){
git credentialsId: '8e9db6b7-9087-4522-94ea-ccfb864d2e47', url: 'https://github.com/classes-101/test-maven.git'
}
stage('install'){
  sh "mvn install"

}
stage('test'){
  sh "mvn test"

}
stage('compile'){
  sh "mvn compile"

}
stage('package'){
  sh "mvn package"

}
}


this will do with scm code also 
PIPELINE>SCm>GIT>url and credentials> jenkinsfile>build now.

this all are kept it in jenkinsfile.

which is included in SCM.


