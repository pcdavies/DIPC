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

### **STEP 8**: Open a terminal and navigate to directory with agent

-   view agent zip file

	![](images/300/AgentImage055-UnzipAgent.png)

-   unzip agent file

	![](images/300/AgentImage060-UnzipAgent.png)


### **STEP 9**: Show current agent page in DIPC console

-   Click "Agent" in the left toolbar
-   There is only one local agent install

	![](images/300/AgentImage065-Current_DIPC_Agent_Page.png)


### **STEP 10**: Identify private IP for DIPC console

-   Note the private IP listed in bottom left of DIPC console

	![](images/300/AgentImage070-DIPC_Priv_IP.png)


### **STEP 11**: Install the Agent from On-Prem Console

-   Open a terminal in On-Prem VM
-   Navigate to the agent directory
-   Execute command to install agent using password - #!hyper1on!#
    ./dicloudConfigureAgent.sh -dipchost=10.0.0.3 -dipcport=7003 -user=weblogic -authType=BASIC

-   Set the "dipchost" parameter to 10.0.0.3
-   This configuration does not have IDCS so use "BASIC" for parameter AuthType

	![](images/300/AgentImage075-Execute_Agent_Install.png)
   
-   Output shows agent created
-   ![](images/300/AgentImage080-Execute_Agent_Install.png)


### **STEP 12**: Modify Agent Parameter 

-   Modify agent port "agentPort" in parameter file "agent.properties" to 7010
path to parameter file: /home/DIPC/Documents/dicloud/agent/dipcagent001/conf 

	![](images/300/AgentImage085-ModifyAgentParameter.png)

	![](images/300/AgentImage086-ModifyAgentParameter.png)

### **STEP 13**: Start Agent

-   Start agent using script

	![](images/300/AgentImage090-StartAgent.png)

	![](images/300/AgentImage091-StartAgent.png)

### **STEP 14**: View Remote Agent in DIPC Console

-   Note the private IP listed in bottom left of DIPC console

	![](images/300/AgentImage095-Confirm_Agent_DIPC_Console.png)

### **STEP 15**: Database Sync

-   Note the private IP listed in bottom left of DIPC console

	![](images/300/AgentImage095-Confirm_Agent_DIPC_Console.png)