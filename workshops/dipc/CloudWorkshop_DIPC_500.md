

# Lab 500: Oracle Data Integration Lab Preparation

1. Login to the VM as DIPC user – Password is “welcome1”

![](images/500/image500_0.png)

2. Log into Data Integration Platform Cloud
- Open your browser
- Click on DIPC Home bookmark or go to your <Ravello Instance
hostname>:7003/dicloud/login.html
- Login with weblogic/password
After a few seconds, the following page should appear –

![](images/500/image500_2.png)

# Task 1: Setup ODI Connections

The connectivity information for this hand-on lab is as follows:

Source Schema/User: DIPC_SRC
OLTP_Schema/User: DIPC_TGT
Passwords: welcome
Server: localhost
Port: 1521
Service: dics12c

The next steps will walk you through how to setup each.

1. Log into Data Integration Platform Cloud
- From your local laptop/desktop start Chrome (you can also continue to
use Chrome on the Ravello instance)
- Go to your <Ravello Instance hostname>:7003/dicloud/login.html
- Login with weblogic/#!hyper1on!#
The following page should appear –

![](images/500/image500_2.png)

2. Click Home

3. Create Source Connection
- Click Create Connection

4. Enter the following information
- Name: Sync Source
- Description – Sales OLTP Source Data
- Agent – localhost:
- Type Oracle – selecting Oracle will expand the Connection Settings
- Hostname: localhost
- Port: 1521
- Username: DIPC_SRC
- Password: welcome
- Service Name: dics12c
- Schema: DIPC_SRC

5. Review Connections settings.

6. Click Test Connection then Save

7. Create Target Connection from the Catalog
- Click on the Create button and select Connection

8. Enter the following information
- Name: Sync Target
- Description – Sales OLTP Replicated Data
- Agent – localhost:
- Type Oracle – selecting Oracle will expand the Connection Settings
- Hostname: localhost
- Port: 1521
- Username: DIPC_TGT
- Password: welcome
- Service Name: dics12c
- Schema: DIPC_TGT

9. Click Test Connection then Save

10. Review Catalog after saving –

11. Data Entities are harvested and profiled at Connection creation, their popularity
is also calculated by reviewing the DB query logs
Note: This process may take some time (5 minutes or so), the Catalog will show
a message when new updates are available


12. Click an entity – SRC_ORDERS
You can browse the Catalog pages to find it or you can use the Search bar
(search for SRC_ for example)

Notice the Popularity score calculated for SRC_ORDERS, a full bar means that this
is one of the Data Entities that has been used the most in queries. Right now
SRC_ORDERS hasn’t been used yet so the bar is empty. Tags can be added as
well to group objects together

13. Click on the Metadata tab

14. Click on an Attribute, ORDER_DATE for example

15. Notice the Profiling statistics appearing in the right-hand side drawer

16. Click Data tab

17. Go back to the main Catalog page – Search for Data Entity –
SRC_ORDER_LINES and click on it in the Quick Search results

18. Click Metadata tab

19. Click on a column, for example column – QTY

20. Notice the Profiling statistics

21. Click Data tab

22. Review other entities as needed

# New - ODI Data Preparation

![](images/500/image500_3.png)


# Task 2 : Create DIPC Synchronize Data Task

![](images/500/image500_5.png)

1. This hands-on lab uses a JDBC utility client that was built specifically for this
demo. This client is NOT part of DIPC, however it does help visualize the
Synchronize Data and ODI Execution Job process.

2. To start this client open a terminal window in the Ravello Console. If needed
press Enter to see the Login window, re-enter the DIPC user password (welcome1) and press Enter or click Unlock

3. Open a Terminal

4. From the home directory execute ./startDIPCDemoClient.sh

5. Once the Synchronize Data task is saved and executed this client will be used
to visually monitory the Replicated Schema, the tables and their row counts

6. Optional: If you are also familiar with ODI Console, you will be able to monitor
the data pump execution from within ODI Console –

7. Optional: Create a new tab within Chrome

8. Optional: Log into ODI Console
- <Ravello Instance Hostname>:7003/odiconsole
- username: SUPERVISOR
- password: welcome1

9. Within the DIPC App Click Home

10. Click Synchronize Data

11. Name your task –Sync Sales Data

12. Description: Sync Schemas - DIPC_SRC to DIPC_TGT

13. Select your source connection and schema
- Connection: Sync Source
- Schema: DIPC_SRC

14. Select your target connection and schema
- Connection: Sync Target
- Schema: DIPC_TGT

15. Leave ‘Include Initial Load’ and ‘Include Replication’ checked under Advanced
Options. These options allow you to optionally enable or disable the initial load
and/or the on-going schema replication

Note: If you run into any issues when trying to select a Connection refresh the page
manually. The Schemas may take some time to appear as well, this is expected.

16. Next click on Configure Entities to filter the objects that will be transferred from
Sync Source into Sync Target

17. The Configure Entities screen allows you to create include or exclude rules to
define precisely which database objects will be moved over to the target
schema. By default all Data Entities are transferred

18. Enter SRC* in the Rules field and click on Include

19. Then click on the menu next to the 1st rule (Include *) and select Delete

20. You should end up with only the following Include Rule (Include SRC*) listed

21. To better view the Demo Client as well as the DIPC monitoring, try to setup your
screen as follows with the Demo Client at the top and the DIPC App below or
have the two side by side.
It is recommended to use two screens if possible.

- Click Save and Run
- A notification will appear that the job was saved.
- A new DIPC Job will be created to executed the task.

A notification will appear in the notification bar as below:

- The job will automatically appear within the Jobs page. This may take
up to 1 minute.
- Click on the Job to see the Job Details
- Auto-refresh is on, statuses will be updated frequently
- As the job executes, the Initial Load process is created in ODI while DIPC
configures OGG for the Source Capture and Target Delivery
- As this job executes, the Replicated Sales OLTP Source Data table will
be updated in the Demo Client. As new tables are created they will show
up as yellow, when the row counts of the source and replicated schemas
match the rows will turn green

Note: It may take several minutes for the Replicated Sales OLTP Data side to
show anything. This is normal.

- As the row counts of each table match the rows will turn green
- Optional: The Initial Load process (uses Data Pump) can also be
monitored within ODI Console- (second created tab in Chrome)
Expand Runtime/Sessions/Load Plan Executions then click on Sessions
and on the glasses icon to view the status
- Optional: Click on the Session at the top of the list to view the Details in
ODI Console
- Once the row counts match and the Initial Load process is complete the
“Initial Load Complete” button within the Demo Client will be enabled.
- Go back to the Job Details in the DIPC App. to review the status there.
The Initial load Action will show Successful after a little while (may take 7
minutes or more)
- Once done, the Initial load Action can be expanded to review the various
Steps underneath
- Click on Procedure:Initial load_PROC:DBLINK_DATAPUMP to review the
Code generated by DIPC for the Initial Load. Click Done when you’ve
completed the code review

# New - ODI Sync and Monitor

![](images/500/image500_6.png)

- Syncronize Data Task
- More Control
- Initial load 
- AND/OR On-going synchronization 
- Data Entity selection using Include/Exclude Rules to only move specific DB objects
- Synchronize Data Jobs can be stopped and restarted
- Uses GoldenGate Pump and now supports 2 Agents


![](images/500/image500_6.png)

# Task 3 : Validate DIPC data Synchronization Job

At this point DIPC has created and orchestrated the initial load and the data
synchronization process for the OLTP source and operational data store. A new DIPC
job is created and executed and can be monitored with the Jobs view.

1. You can also monitor the process by monitoring the DIPC Agent terminal
window. You could also monitor the DIPC Managed Server, however there is a
lot of detailed information here

2. Click Jobs and refresh until the newly created DIPC Job shows up.
a. You should see 5 Actions

3. The DIPC agent is orchestrating this process. Additional details can be seen in
the GG logs as well as within ODI Studio.

4. Before doing anything else monitor GG and watch for extracts and replicats to
be created and started and RUNNING
- Open Terminal on DIPC host machine
- cd /home/DIPC
- Execute ./GGINFO_ALL.sh
- Ensure both Extract and Replicat are running

5. Once all rows are green in the Demo Client, proceed to next step

# NEW! : ODI Execution

1. Easily execute ODI scenario!

2. Easily monitor ODI scenario!

3. Support hybrid development mode

- Develop / design on-prem
- Import to Data Integration Platform and integrate with DIPC Tasks
- Execute and monitor ODI Job in DIPC Console
- Supports Technologies currently supported in DIPC

# NEW! : Introducing Autonomous Data Integration Platform (ADIPC)

![](images/500/image500_7.png)

- Coming soon to an OCI data center near you!


# Summary

You have now successfully completed the Hands on ODI Preparation Lab
