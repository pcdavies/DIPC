![](images/300/AgentImage05-SplashScreen.JPG)

Update: Apr 25, 2018

## Introduction - Remote Agent Install and Synchronization of an On-prem database

This lab covers installation and configuration of DIPC remote agent along with synchronization of an on-prem database. Agents allow synchronization of data from sources outside Oracle Cloud. Two VMs within Ravello will be used to simulate a DIPC instance and an On-Prem database server.

This lab supports the following use cases:
-   Configure Remote DIPC Agent
-   Synchronize On-Premise Database

## Objectives

-   Ensure Ravello VMs for DIPC and DB 
-	Ensuring Remote Agent is trusted by DIPC instance
-   Agent Download
-   Agent Installation and Configuration
-   Configure Agent SSL
-	Agent Administration - Starting and Stopping.
-   Synchronize On-Premise Database
   
### **STEP 1**: Identify Shared Ravello Blueprint

-   In the Left Sidebar Click on Library>Blueprints

	![](images/300/AgentImage010-IdentifyBlueprint.png)

AgentImage015-CreateApplication.png

### **STEP 2**: Create Ravello Application

-   Click "Create Application"

	![](images/300/AgentImage015-CreateApplication.png)

-   Enter Ravello Application Details
    Name: "DIPC 18.2.3 Agent - DB Sync"
    Description: "DIPC Agent - DB Sync Configuration"
    Click "Create"

	![](images/300/AgentImage020-ReviewAppConfig.png)

### **STEP 3**: Publish Ravello Application

-   Publish the Blueprint VMs
    Click "Publish" highlighted in top right

	![](images/300/AgentImage025-PublishApp.png)

-   Review publish parameters and click "Publish"
    
	![](images/300/AgentImage030-ReviewPublishApp.png)


### **STEP 4**: Log into DIPC Console and go to Agent Page

-   Click "Agents" in left panel

	![](images/300/AgentImage035-HomePage.JPG)

### **STEP 5**: Select Download Installer Drop Down Menu

-   Select drop down menu and select zip file for your Operating System

	![](images/300/AgentImage040-DownloadAgent.JPG)

### **STEP 6**: Confirm your agent download selection

-   Click "OK" to confirm selection

	![](images/300/AgentImage045-DownloadAgent.JPG)

### **STEP 7**: Save the agent zip file to your home directory

-   Save the file to your home directory in preparation to unzip and install

	![](images/300/AgentImage050-DownloadAgentSave.JPG)


