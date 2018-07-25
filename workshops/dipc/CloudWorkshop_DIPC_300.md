# Lab 300 - Remote Agent Install and On-prem to On-prem DB Synchronization

![](images/300/image300_0.png)

## Before You Begin

### Introduction - 

This lab covers installation and configuration of DIPC remote agent along with synchronization of two on-prem database schemas. Agents allow synchronization of data from sources outside Oracle Cloud. The target and source schemas will reside in the same database.

This lab supports the following use cases:
-   Configure Remote DIPC Agent
-   Synchronize two On-Premise Databases

### Objectives
-	Ensure Remote Agent is trusted by DIPC instance
-   Agent Download
-   Agent Installation and Configuration
-	Agent Administration - Starting and Stopping.
-   Synchronize two On-Premise Databases
   
### Time to complete
Approximately 45 minutes.

### What would you need
-   Cloud Dashboard URL and login credentials
-   1 DIPC Instance - DIPCINST
-   2 DBCS Instances - DBCSAMER, DBCSEMEA
-   1 Compute Instance - OnPremiseVM
-   Private keys in OpenSSH format for all instances 
-   OnPremiseVM public IP address
-   VNC Client
-	Putty for ssh connection to instances

## Remote Agent

### Download Agent
1.	Open an SSH session into your compute server (we will simulate on-prem with a compute instance); please refer to Appendix 1 to learn how to establish a SSH session
2.	Open a VNC viewer; please refer to Appendix 2 to learn how to establish a VNC session
3.	Open a terminal; select “Applications > Favorites > Firefox” from the top left corner of the screen

![](images/300/image300_1.png)
 
4.	Navigate to your DIPC server, provide the URL (it should look like this): https://osc132657dipc-oscnas001.uscom-central-1.oraclecloud.com/dicloud
5.	Provide your user name and password, then click "Sign In" button

![](images/300/image300_2.png)
 
6.	This will bring you to your DIPC server’s  home page
7.	Click on “Agents” (left part of your screen)

![](images/300/image300_3.png)

8.	Select drop down menu and select zip file for your Operating System 
9.	Select the “Linux” option

![](images/300/image300_4.png)

10.	Click "OK" to confirm selection

![](images/300/image300_5.png)
 
11.	Select “Save File” and the click “OK”, to download the file to your “on-premise” machine

![](images/300/image300_6.png)

12.	Open a terminal, select “Applications > Favorites > Terminal” from the top left corner of the screen

![](images/300/image300_7.png)

### Install Agent
1.	Create a directory for the agent, execute: mkdir dipcagent
2.	Move the downloaded file to that new directory, execute: mv Downloads/* dipcagent
3.	MOve to the new directory, execute: cd dipcagent
4.	Unzip the file, execute: unzip agent-linux.64.bit.zip
5.	Move to the agent directory, execute: cd dicloud
6.	Execute command to install agent: 
./dicloudConfigureAgent.sh -user=DIPCADMIN -dipchost=<DIPC_IP_ADDRESS> -dipcport=7003  -authType=BASIC
7.	New directories will be created, to look at then execute: ls
8.	We will take a look at the configuration file (agent.properties) and we will change the port in which this agent will talk to DIPC
9.	Open the editor, select “Applications > Accessories > Editor” from the top left corner of the screen

![](images/300/image300_9.png)
 
10.	Click on “Open” then “Other Documents”

![](images/300/image300_10.png)

11.	Browse to “/home/oracle/dipcagent/dicloud/agent/dipcagent001/conf/agent.properties”

![](images/300/image300_11.png)
 
12.	Modify agent port "agentPort" in parameter file "agent.properties" to 7010

![](images/300/image300_12.png)
 
13.	Now look for “ggccServicePort” and change it to 80

![](images/300/image300_13.png)
 
14.	Save and close. Click on “Save” button then on "Close" icon (top right corner)

### Execute the Agent
1.	We installed with defaults so we will move to the directory with the necessary commands to start the agent; execute: cd agent/dipcagent001/bin
2.	We will start the agent by executing:
./startAgentInstance.sh
3.	Your agent is now running. Go back to Firefox and look the “Agent” screen in DIPC
 
![](images/300/image300_14.png)


## On-Prem to On-Prem synchronization

### Verify







### **STEP 12**: [OnPremiseVM] Review On-Prem Schema

-   Connect to remote schema and view tables and row count


	![](images/300/AgentImage100-ReviewOnPremSchema.png)

### **STEP 13**: [DIPC 18.2.3] Create Source Connection to On-Prem Schema

-   Navigate to DIPC console
-   Click "Home" in left toolbar and click "Create Connections"


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


### **STEP 14**: [OnPremiseVM] Create blank target Schema ONPREM_TRG

-   Create schema and ensure necessary privileges
-   SQL> create user onprem_trg identified by welcome1;
-   SQL> grant connect, resource, unlimited tablespace to onprem_trg;
-   SQL> grant create database link to onprem_trg;
-   
-   View schema tables and row count - should be empty
-   SQL> connect onprem_trg
-   SQL> select table_name from user_tables;

	![](images/300/AgentImage115-OnpremTrgSchema.png)


### **STEP 15**: [DIPC 18.2.3] Create Target Connection to Schema ONPREM_TRG

-   Enter target connection information to schema ONPREM_TRG
-   Use same remote agent on port 7010 for target connection

    - Name:        ONPREM_TRG
    - Description: Connection to target schema onprem_trg
	- Agent:       localhost:7010
	- Type:        Oracle
	- Connection Settings
	  - Hostname:   localhost
	  - Port:       1521
	  - Username:   ONPREM_TRG
	  - Password:   welcome1
	  - Service:    Service Name: dics12c

-   Click "Test Connection"

	![](images/300/AgentImage120-CreateOnpremTargetConnection.png)

-   Click "Save" to save target connection

	![](images/300/AgentImage121-TestSaveTargetConnection.png)

-   View Target Connection

	![](images/300/AgentImage122-ViewTargetConnection.png)

### **STEP 16**: [DIPC 18.2.3] Create Sync Job between Source and Target

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
	  - Connection: ONPREM_TRG
	  - Schema: ONPREM_TRG
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

