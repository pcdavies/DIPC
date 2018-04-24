

This is derived from the Ravello Image recently released as of 4.24.2018 –

# Task 0: Preparation Steps

_In these steps you will clean up and setup the environment for this exercise_

1. Login to the VM as DIPC user – Password is “welcome1”

![](images/200/image200_1.png)

2. Log into Data Integration Platform Cloud
a. Open your browser
b. Click on DIPC Home bookmark or go to your <Ravello Instance
hostname>:7003/dicloud/login.html
c. Login with weblogic/password
After a few seconds, the following page should appear –

3. Setup/ Download Agent/ GG Setup
DIPC On-Premise Agents allow synchronizing data from outside of Oracle
Public Cloud.
a. For this download we will use Chrome running in the VM not the one
running on your laptop/desktop
b. Go to Applications > Internet and click Google Chrome
c. Note: If Chrome ask for keyring password then enter “welcome1”
d. In Chrome, click on DIPC Home bookmark or go to
localhost:7003/dicloud/login.html
e. Login with weblogic/password
f. Click Agents
g. Click Download Installer then select Linux 64 - bit
h. Click OK in the Download Agent Installer window
i. Create the DIPC_AGENT2 directory and click on Save
j. Extract agent.zip to ~/DIPC_AGENT
i. Click on downloaded file within Chrome
ii. Extract with Unzip UI
iii. Click Extract again (blue button)
iv. Close all Unzip UI windows
k. Open a new Terminal window
l. cd /home/DIPC/DIPC_AGENT2/dicloud
m. Execute ./dicloudConfigureAgent.sh -dipchost=localhost -dipcport=7003 -
user=weblogic - authType=BASIC
n. Script will prompt for password - password
o. cd /home/DIPC/DIPC_AGENT2/dicloud/agent/dipcagent001/conf
p. vi agent.properties
i. Use “i” to turn insert mode on
ii. Change agent port (agentport) to 7009 since default is already
used
iii. Change GG manager port (gginstanceport) to 7919 since default is
already used
iv. Hit ESC then :wq to save
q. cd /home/DIPC/DIPC_AGENT2/dicloud/agent/dipcagent001/bin
r. Execute ./startAgentInstance.sh
In the Terminal window you should see ‘NOTIFICATION Done.
GoldenGate manager is configured now.’ when the Agent is fully started
s. In Browser : Within app, on your desktop go to Agents page in DIPC
t. The new agent should appear as follows (it will be Stopped at first then
Running):

# Task 1: Setup DIPC Connections

The connectivity information for this hand-on lab is as follows:

Source Schema/User: DIPC_SRC
OLTP_Schema/User: DIPC_TGT
Passwords: welcome
Server: localhost
Port: 1521
Service: dics12c

The next steps will walk you through how to setup each.

1. Log into Data Integration Platform Cloud
a. From your local laptop/desktop start Chrome (you can also continue to
use Chrome on the Ravello instance)
b. Go to your <Ravello Instance hostname>:7003/dicloud/login.html
c. Login with weblogic/#!hyper1on!#
The following page should appear –

2. Click Home

3. Create Source Connection
a. Click Create Connection

4. Enter the following information
a. Name: Sync Source
b. Description – Sales OLTP Source Data
c. Agent – localhost:
d. Type Oracle – selecting Oracle will expand the Connection Settings
e. Hostname: localhost
f. Port: 1521
g. Username: DIPC_SRC
h. Password: welcome
i. Service Name: dics12c
j. Schema: DIPC_SRC

5. Review Connections settings.

6. Click Test Connection then Save

7. Create Target Connection from the Catalog
a. Click on the Create button and select Connection

8. Enter the following information
a. Name: Sync Target
b. Description – Sales OLTP Replicated Data
c. Agent – localhost:
d. Type Oracle – selecting Oracle will expand the Connection Settings
e. Hostname: localhost
f. Port: 1521
g. Username: DIPC_TGT
h. Password: welcome
i. Service Name: dics12c
j. Schema: DIPC_TGT

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

# Task 2 : Create DIPC Synchronize Data Task

1. This hands-on lab uses a JDBC utility client that was built specifically for this
demo. This client is NOT part of DIPC, however it does help visualize the
Synchronize Data and ODI Execution Job process.

2. To start this client open a terminal window in the Ravello Console. If needed
press Enter to see the Login window, re-enter the DIPC user password

(welcome1) and press Enter or click Unlock

3. Open a Terminal

4. From the home directory execute ./startDIPCDemoClient.sh

5. Once the Synchronize Data task is saved and executed this client will be used
to visually monitory the Replicated Schema, the tables and their row counts

6. Optional: If you are also familiar with ODI Console, you will be able to monitor
the data pump execution from within ODI Console –

7. Optional: Create a new tab within Chrome

8. Optional: Log into ODI Console
a. <Ravello Instance Hostname>:7003/odiconsole
b. username: SUPERVISOR
c. password: welcome

9. Within the DIPC App Click Home

10. Click Synchronize Data

11. Name your task –Sync Sales Data

12. Description: Sync Schemas - DIPC_SRC to DIPC_TGT

13. Select your source connection and schema
a. Connection: Sync Source
b. Schema: DIPC_SRC

14. Select your target connection and schema
a. Connection: Sync Target
b. Schema: DIPC_TGT

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

## OR

22. Run Synchronize Data Task
a. Click Save and Run
b. A notification will appear that the job was saved.
c. A new DIPC Job will be created to executed the task.

A notification will appear in the notification bar as below:

d. Tthe job will automatically appear within the Jobs page. This may take
up to 1 minute.
e. Click on the Job to see the Job Details
f. Auto-refresh is on, statuses will be updated frequently
g. As the job executes, the Initial Load process is created in ODI while DIPC
configures OGG for the Source Capture and Target Delivery
h. As this job executes, the Replicated Sales OLTP Source Data table will
be updated in the Demo Client. As new tables are created they will show
up as yellow, when the row counts of the source and replicated schemas
match the rows will turn green

Note: It may take several minutes for the Replicated Sales OLTP Data side to
show anything. This is normal.

i. As the row counts of each table match the rows will turn green
j. Optional: The Initial Load process (uses Data Pump) can also be
monitored within ODI Console- (second created tab in Chrome)
Expand Runtime/Sessions/Load Plan Executions then click on Sessions
and on the glasses icon to view the status
k. Optional: Click on the Session at the top of the list to view the Details in
ODI Console
l. Once the row counts match and the Initial Load process is complete the
“Initial Load Complete” button within the Demo Client will be enabled.
m. Go back to the Job Details in the DIPC App. to review the status there.
The Initial load Action will show Successful after a little while (may take 7
minutes or more)
n. Once done, the Initial load Action can be expanded to review the various
Steps underneath
o. Click on Procedure:Initial load_PROC:DBLINK_DATAPUMP to review the
Code generated by DIPC for the Initial Load. Click Done when you’ve
completed the code review

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
a. Open Terminal on DIPC host machine
b. cd /home/DIPC
c. Execute ./GGINFO_ALL.sh
d. Ensure both Extract and Replicat are running

5. Once all rows are green in the Demo Client, proceed to next step

# Task 4 : Monitor Source Inserts/Updates/Deletes

1. Now that the initial load is complete and the extract/replicat have been created
and are running, we can simulate insert/updates and deletes on the source and
monitor the replicated data through the Demo Client.

2. Using the Demo Client click on the “Initial Load Complete” Button.

3. The following screen will appear. NOTE – the current refresh of the client is 10
seconds.

The demo client shows the source Sales OLTP data, the replicated Sales OLTP
data, and the target Sales DW. As data is updated, inserted or deleted from the
source the data will be automatically synchronized with the replicated schema
by the Sync Sales Data Job we created in DIPC. Once the synchronization is
done, the target Sales DW schema is updated by a scenario that was created in
the Standalone ODI Instance included with DIPC. DIPC and standalone ODI will
work hand in hand to implement the end-to-end data flow.
Note: We will be using an ODI Execution Task in DIPC to kick off the execution
of that scenario

Note: If the window is too small through the Ravello Console you can also use
VNC to log into the VM. Use your favorite VNC client and enter <Ravello
Instance Hostname>:1 as the URL to connect to.
When prompted enter the password: #DIPCR0CKS#

4. Perform a simple update of the source table by editing the data directly within
the table grid. Update the first row’s status which contains ORDER_ID=1 from
COM to CLO, clicking enter will commit the update and turn the column yellow –

5. This row will be automatically update on the replicated schema as the DIPC Job
picks up the change. The Demo Client is set to refresh at 10 seconds, so it will
at least take 10 seconds for the replicated table grid to update. Once the Demo
Client finds the change both rows will be updated to yellow.

6. The yellow highlights will automatically expire within the client.

7. To perform an insert click on the “Simulate Inserts” Button once.
This will perform an insert and the demo client will scroll to the row that was
inserted.

8. Depending on the refresh, the row may directly be replicated to the replicated
schema or appear in the next refresh by the Demo Client.

9. Both rows should show as yellow

10. To perform a delete click last row and click on the icon. Notice this record
will be delete from the replicated schema as well.

# Summary

You have now successfully completed the Hands on Lab, and have successfully performed an
end-to-end data synchronization task through Oracle’s Data Integration Platform Cloud.

