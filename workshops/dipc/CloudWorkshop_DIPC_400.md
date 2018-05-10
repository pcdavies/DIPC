![](images/400/AgentImage05-WorkshopHeader.PNG)

Update: May 10, 2018

## Introduction - Remote Agent Install and Synchronization of an On-prem database

This lab covers installation and configuration of DIPC remote agent along with synchronization of an on-prem database. Agents allow synchronization of data from sources outside Oracle Cloud. Two VMs within Ravello will be used to simulate a DIPC instance and an On-Prem database server. 
Ravello VMs are being used to simulate cloud instances and do not have Identity Cloud Service (IDCS). Modifications will be made before porting to a GSE environment.

This lab supports the following use cases:
-   Configure Remote DIPC Agent
-   Synchronize On-Premise Database

## Objectives

-   Ensure Ravello VMs for DIPC and DB 
-	Ensure Remote Agent is trusted by DIPC instance *MODIFY FOR GSE*
-   Agent Download
-   Agent Installation and Configuration
-   Configure Agent SSL *MODIFY FOR GSE*
-	Agent Administration - Starting and Stopping.
-   Synchronize On-Premise Database
   
### **STEP 1**: Identify Shared Ravello Blueprint *REMOVE FOR GSE*

-   In the Left Sidebar Click on Library>Blueprints

	![](images/400/AgentImage010-IdentifyBlueprint.png)

### **STEP 2**: Create Ravello Application  *REMOVE FOR GSE*

-   Select Blueprint "DIPC 18.2.3 V6-bp Werner 4.6.2018"
-   Click "Create Application"

	![](images/400/AgentImage015-CreateApplication.png)

-   Enter Ravello Application Details
    Name: "DIPC 18.2.3 Agent - DB Sync"
    Description: "DIPC Agent - DB Sync Configuration"
    Click "Create"

	![](images/400/AgentImage020-ReviewAppConfig.png)

### **STEP 3**: Publish Ravello Application

-   The Blue Print has two VMs: "DIPC 18.2.3" & "DIPC 18.2.3.1"
-   Change "DIPC 18.2.3.1" to "On-Prem DB Svr"
-   Publish the Blueprint VMs
    Click "Publish" highlighted in top right

	![](images/400/AgentImage025-PublishApp.png)

-   Review publish parameters and click "Publish"
-   Choose "Performance" for Optimize option
-   Start the VMs and Log into the Consoles using:
    -  Username/Password: DIPC/wecome1
    
	![](images/400/AgentImage030-ReviewPublishApp.png)


### **STEP 4**: [DIPC 18.2.3] Log into DIPC Console and go to Agent Page

-   From "DIPC 18.2.3" lauch DIPC Console from Chrome browser bookmark
-   Login using:
    - Username/Password: weblogic/welcome1
-   Click "Agents" in left panel

	![](images/400/AgentImage035-HomePage.JPG)

### **STEP 5**: [DIPC 18.2.3] Select Download Installer Drop Down Menu

-   Select drop down menu and select zip file for your Operating System

	![](images/400/AgentImage040-DownloadAgent.JPG)

### **STEP 6**: [DIPC 18.2.3] Confirm your agent download selection

-   Click "OK" to confirm selection

	![](images/400/AgentImage045-DownloadAgent.JPG)

### **STEP 7**: [DIPC 18.2.3] Save the agent zip file to your home directory

-   Save the file to your home directory in preparation to unzip and install
-   ftp agent zip file to "On-Prem DB Svr"

	![](images/400/AgentImage050-DownloadAgentSave.JPG)

### **STEP 8**: [On-Prem DB Svr] View and unzip agent file

-   Open terminal on "On-Prem DB Svr]
-   view agent zip file "agent-linux.64.bit.zip"

	![](images/400/AgentImage055-UnzipAgent.png)

-   unzip agent file
    -   $unzip agent-linux.64.bit.zip

	![](images/400/AgentImage060-UnzipAgent.png)


### **STEP 9**: [DIPC 18.2.3] Show current agent page in DIPC console

-   Navigate to DIPC console on VM "DIPC 18.2.3"
-   Click "Agent" in the left toolbar
-   There is only one local agent install 


	![](images/400/AgentImage065-Current_DIPC_Agent_Page.png)


### **STEP 10**: [DIPC 18.2.3] Identify private IP for DIPC console

-   Navigate to Ravello Application to get information for agent install
-   Click VM "DIPC 18.2.3" (DIPC Instance and Target DB)
-   Note the private IP listed in bottom left of DIPC console (10.0.0.3)


	![](images/400/AgentImage070-DIPC_Priv_IP.png)


### **STEP 11**: [On-Prem DB Svr] Install the Agent from On-Prem Console

-   Open a terminal in On-Prem VM
-   Navigate to the agent directory
-   Execute command to install agent using password - #!hyper1on!#
    ./dicloudConfigureAgent.sh -dipchost=10.0.0.3 -dipcport=7003 -user=weblogic -authType=BASIC

-   Set the "dipchost" parameter to 10.0.0.3
-   This configuration does not have IDCS so use "BASIC" for parameter AuthType


	![](images/400/AgentImage075-Execute_Agent_Install.png)
   
-   Output shows agent created

-   ![](images/400/AgentImage080-Execute_Agent_Install.png)


### **STEP 12**: [On-Prem DB Svr] Modify Agent Parameter 

-   Modify agent port "agentPort" in parameter file "agent.properties" to 7010
-   path to parameter file: 
-   /home/DIPC/Documents/dicloud/agent/dipcagent001/conf 


	![](images/400/AgentImage085-ModifyAgentParameter.png)

	![](images/400/AgentImage086-ModifyAgentParameter.png)

### **STEP 13**: [On-Prem DB Svr] Start Agent

-   Navigate to the agent bin directory
    -   /home/DIPC/Documents/dicloud/agent/dipcagent001/bin
-   Start agent using script startAgentInstance.sh
    -   $ ./startAgentInstance.sh


	![](images/400/AgentImage090-StartAgent.png)

	![](images/400/AgentImage091-StartAgent.png)

### **STEP 14**: [DIPC 18.2.3] View Remote Agent in DIPC Console

-   Navigate to DIPC Console
-   Clict Agents in left toolbar


	![](images/400/AgentImage095-Confirm_Agent_DIPC_Console.png)

### **STEP 15**: [DIPC 18.2.3] Ensure local and Remote Agents are started

-   Start agents as needed from Agent bin directory
    -   $ ./startAgentInstance.sh


	![](images/400/AgentImage096-Confirm_SRC_TRG_Agent_Started.png)

### **STEP 16**: [On-Prem DB Svr] Review On-Prem Schema

-   Connect to remote schema and view tables and row count


	![](images/400/AgentImage100-ReviewOnPremSchema.png)

### **STEP 17**: [DIPC 18.2.3] Create Source Connection to On-Prem Schema

-   Navigate to DIPC console
-   Click Home in left toolbar and click "Create Connections"


	![](images/400/AgentImage101-CreateSourceConnection.png)

-   Enter source connection information for On-prem schema

    - Name:        ONPREM_SRC
    - Description: Connection to on-prem database schema with source tables
	- Agent:       localhost:7010
	- Type:        Oracle
	- Connection Settings
	  - Hostname:   10.0.0.4
	  - Port:       1521
	  - Username:   DIPC_SRC
	  - Password:   welcome1
	  - Service:    Service Name: dics12c


	![](images/400/AgentImage105-EnterSrcConnectionInfo.png)

-   Click "Test Connection" and "Save"

	![](images/400/AgentImage105-TestSaveSrcConnection.png)

-   Search for source connection ONPREM_SRC in catalog

	![](images/400/AgentImage110-SearchConnectionCatalog.png)

    ![](images/400/AgentImage111-ViewSrcConnectionCatalog.png)

-   Click connection name to view summary

    ![](images/400/AgentImage112-ViewSrcConnectionSummary.png)

-   Click metadata tab

    ![](images/400/AgentImage113-ViewSrcConnectionMetadata.png)


### **STEP 18**: [DIPC 18.2.3] Create blank target Schema CLOUD_TRG

-   Create schema and ensure necessary privileges
-   SQL> create user cloud_trg identified by welcome1;
-   SQL> grant connect, resource, unlimited tablespace to cloud_trg;
-   SQL> grant create database link to cloud_trg;
-   

	![](images/400/AgentImage115-TargetSchema.png)

-   View schema tables and row count - should be empty

	![](images/400/AgentImage116-ViewTargetSchema.png)


### **STEP 19**: [DIPC 18.2.3] Create Target Connection to Schema CLOUD_TRG

-   Enter target connection information to schema CLOUD_TRG

    - Name:        CLOUD_TRG
    - Description: Connection to target schema cloud_trg
	- Agent:       localhost:7009
	- Type:        Oracle
	- Connection Settings
	  - Hostname:   localhost
	  - Port:       1521
	  - Username:   CLOUD_TRG
	  - Password:   welcome1
	  - Service:    Service Name: dics12c

-   Click "Test Connection"

	![](images/400/AgentImage120-CreateTargetConnection.png)

-   Click "Save" to save target connection

	![](images/400/AgentImage121-SaveTargetConnection.png)

-   View Target Connection

	![](images/400/AgentImage122-ViewTargetConnection.png)

### **STEP 20**: [DIPC 18.2.3] Create Sync Job between Source and Target

-   In DIPC Console click "Home" in left toolbar
-   Click "Synchronize Data"

	![](images/400/AgentImage125-CreateSyncJob.png)

-   Enter Sync Job Information
    - General Information
	  - Name:        SYNC ONPREM SCHEMA
	  - Description: Job to sync on-prem schema with cloud target schema
	- Source Configuration
	  - Connection: ONPREM_SRC
	  - Schema:     DIPC_SRC
	- Target Configuration
	  - Connection: CLOUD_TRG
	  - Schema: CLOUD_TRG
	- Advanced Options
	  - Include Initial Load: check for initial load
	  - Include Replication: check for replication

-   Click "Save & Run"

	![](images/400/AgentImage125-EnterSynJobInfo.png)

-   Click Job to review Sync Job Details

	![](images/400/AgentImage130-SyncJobMonitor.png)

-   Monitor Target Schema for table creation and row count
AgentImage135-SyncJobMonitorSchema.png

	![](images/400/AgentImage135-SyncJobMonitorSchema.png)

	![](images/400/AgentImage136-SyncJobMonitorSchema2.png)

	![](images/400/AgentImage137-SyncJobMonitorSchema3.png)

