![](images/300/AgentImage05-WorkshopHeader.PNG)

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

-   Clict Agents in left toolbar

	![](images/300/AgentImage095-Confirm_Agent_DIPC_Console.png)

### **STEP 15**: Ensure local and Remote Agents are started

-   Start agents as needed from Agent bin directory


	![](images/300/AgentImage096-Confirm_SRC_TRG_Agent_Started.png)


### **STEP 16**: Review On-Prem Schema

-   Connect to remote schema and view tables and row count


	![](images/300/AgentImage100-ReviewOnPremSchema.png)

### **STEP 17**: Create Source Connection to On-Prem Schema

-   Click Home in left toolbar and click "Create Connections"


	![](images/300/AgentImage101-CreateSourceConnection.png)

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


	![](images/300/AgentImage105-EnterSrcConnectionInfo.png)

-   Click "Test Connection" and "Save"

	![](images/300/AgentImage105-TestSaveSrcConnection.png)

-   Search for source connection ONPREM_SRC in catalog

	![](images/300/AgentImage110-SearchConnectionCatalog.png)

    ![](images/300/AgentImage111-ViewSrcConnectionCatalog.png)

-   Click connection name to view summary

    ![](images/300/AgentImage112-ViewSrcConnectionSummary.png)

-   Click metadata tab

    ![](images/300/AgentImage113-ViewSrcConnectionMetadata.png)


### **STEP 18**: Create blank target Schema CLOUD_TRG

-   Create schema and ensure necessary privileges

	![](images/300/AgentImage115-TargetSchema.png)

-   View schema tables and row count - should be empty

	![](images/300/AgentImage116-ViewTargetSchema.png)


### **STEP 19**: Create Target Connection to Schema CLOUD_TRG

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

	![](images/300/AgentImage120-CreateTargetConnection.png)

-   Click "Save" to save target connection

	![](images/300/AgentImage121-SaveTargetConnection.png)

-   View Target Connection

	![](images/300/AgentImage122-ViewTargetConnection.png)

### **STEP 20**: Create Sync Job between Source and Target

-   In DIPC Console click "Home" in left toolbar
-   Click "Synchronize Data"

	![](images/300/AgentImage125-CreateSyncJob.png)

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

	![](images/300/AgentImage125-EnterSynJobInfo.png)

-   Click Job to review Sync Job Details

	![](images/300/AgentImage130-SyncJobMonitor.png)

-   Monitor Target Schema for table creation and row count
AgentImage135-SyncJobMonitorSchema.png

	![](images/300/AgentImage135-SyncJobMonitorSchema.png)

	![](images/300/AgentImage136-SyncJobMonitorSchema2.png)

	![](images/300/AgentImage137-SyncJobMonitorSchema3.png)

