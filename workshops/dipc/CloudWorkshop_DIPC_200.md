
# Lab 200 - Data Synch Elevated Task
![](images/200/image200_0.png)

## Before You Begin

### Purpose
This lab shows you how to execute a Data Synch elevated task; as well as how to define all necessary elements to run the task.

### Time to Complete 
Approximately 60 minutes.

### What Do You Need?
Your will need:
- DIPC Instance URL
- DIPC User and Password
- General understanding of RDBMS and data integration concepts

## Log into DIPC Server

### Login into DIPC using Oracle Cloud Services Dashboard
1. In your web browser, navigate to cloud.oracle.com, then click Sign in.
2. Provide the cloud account: oscnas001 then <Enter>
3. Provide your user name and password, then click "Sign In" button. You will land in the Dasboard screen

	![](images/200/image200_1.png)

4. In the "Data Integration Platform Cloud" service box click on the hamburguer menu and then select "Open Service Console"

![](images/200/image200_1a.png)

5. Click on the hamburger menu of the DIPC server assigned to you, then click "Data Integration Platform Console"

![](images/200/image200_1b.png)

You will be navigated to your DIPC server Home page.

![](images/200/image200_9.png)

### Login into DIPC using direct URL
1. Open a browser window an provide your DIPC server URL. The URL will be provided by the instructor and will look like this one

https://osc132657dipc-oscnas001.uscom-central-1.oraclecloud.com/dicloud

2. Provide your user name and password, then click "Sign In" button

![](images/200/image200_1.png)

You will be navigated to your DIPC server Home page.


## Create Connections and Review Catalog
1. Log into your Workshop DIPC Server
2.	In the Home Page click “Create Connection” from top section
![](images/200/image200_9a.png)

3.	Enter the following information:
    - Name: DIPC_SRC
    - Description: Sales OLTP Source Data
    - Agent: \<LOCAL_AGENT>
    - Type Oracle: selecting Oracle will expand the Connection Settings

    ![](images/200/image200_9b.png)

    - Hostname: <SOURCE_DB>
    - Port: 1521
    - Username: DIPC_SRC
    - Password: Welcome#123
    - Service Name: <SOURCE_DB_SERVICE_NAME>
    - Schema: DIPC_SRC
    - Schema Name: DIPC_SRC (Default) – When you try to select the schema, you are testing the connection at the same time
    - CDB Connection: SRC_CDB

    ![](images/200/image200_10.png)

4. Click "Test Connection" button and when the test is successful click "Save" button. DIPC will create the connection and will harvest the entities in the schema. You will be navigated to the Catalog and you will see, after some time, the connection you just created and the entities in that schema

**Note: Data Entities are harvested and profiled at the time the connection is created, their popularity is also calculated by reviewing the DB query logs. This process may take some time (5 minutes or so), the Catalog will show a message when new updates are available**

![](images/200/image200_10a.png)

5.	Click on entity “SRC_CUSTOMER” to drill down in it and look at the information DIPC brought in

![](images/200/image200_10b.png) 

If you would like to associate a tag or a contact to this entity, click on “Edit” button on the top right corner.

6.	Click on the “Metadata” tab on top

![](images/200/image200_10c.png) 

DIPCS shows attributes, primary keys, data types and some sample values of the selected entity. If you click in one of the attributes, profiling information will be shown on the right side of the screen.

![](images/200/image200_10d.png)  

7.	Click on the “Data” tab on top

![](images/200/image200_10e.png) 

8.	Click on the back icon, located on the top left corner (left of the entity name) to go back to the Catalog
9.	In the catalog you can use the drop-down menu located at the top to select the type of object that will be shown

![](images/200/image200_10f.png)

10.	It is also possible to use the filter to search for a specific object

![](images/200/image200_10g.png)

11.	Now, we are going to create the target connection. From the top bar, Open the drop-down menu from the top far right corner and then select “Connection” 

![](images/200/image200_10h.png)

12.	Enter the following information:
    - Name: DIPC_TGT
    - Description: Sales OLTP Replicated Data
    - Agent: <LOCAL_AGENT>
    - Type Oracle – selecting Oracle will expand the Connection Settings
    - Hostname: <TARGET_DB>
    - Port: 1521
    - Username: DIPC_TGT
    - Password: Welcome#123
    - Service Name: <SOURCE_DB_SERVICE_NAME>
    - Schema: DIPC_TGT (Default)

![](images/200/image200_11.png)

13. Click "Test Connection" button and when the test is successful click "Save" button. DIPC will create the connection and will harvest the entities in the schema. You will be navigated to the Catalog and you will see, after some time, the new connection you just created and the entities in that schema (if any)




## Create Synchronize Data Elevated Task

1. This hands-on lab uses a JDBC utility client that was built specifically for this
demo. This client is NOT part of DIPC, however it does help visualize the
Synchronize Data and ODI Execution Job process.

   a. Open a browser window from your laptop/desktop (not inside the DIPC VM)

    b. Click on DIPC Home bookmark or go to  \<hostname>:7003/dicloud/login.html and sign in
    ![](images/200/image200_3.png)

3. Open a Terminal

![](images/200/image200_21.png)

4. From the home directory execute ./startDIPCDemoClient.sh

![](images/200/image200_22.png)
![](images/200/image200_23.png)

5. Once the Synchronize Data task is saved and executed this client will be used
to visually monitor the Replicated Schema, the tables and their row counts

6. Optional: If you are also familiar with ODI Console, you will be able to monitor
the data pump execution from within ODI Console –

7. Optional: Create a new tab within Chrome

8. Optional: Log into ODI Console
    - \<hostname>:7003/odiconsole
    - username: SUPERVISOR
    - password: welcome 

9. Within the DIPC App, click Home (from the left-most panel)

10. Click Synchronize Data

![](images/200/image200_24.png)

11. Name your task –Sync Sales Data

12. Description: Sync Schemas - DIPC_SRC to DIPC_TGT

![](images/200/image200_25.png)

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

![](images/200/image200_26.png)

16. Next click on Configure Entities to filter the objects that will be transferred from
Sync Source into Sync Target

![](images/200/image200_27.png)

17. The Configure Entities screen allows you to create include or exclude rules to
define precisely which database objects will be moved over to the target
schema. By default all Data Entities are transferred

![](images/200/image200_28.png)

18. Enter SRC* in the Rules field and click on Include

![](images/200/image200_29.png)

19. Then click on the menu next to the 1st rule (Include *) and select Delete

![](images/200/image200_30.png)

20. You should end up with only the following Include Rule (Include SRC*) listed

![](images/200/image200_31.png)

21. To better view the Demo Client as well as the DIPC monitoring, try to setup your
screen as follows with the Demo Client at the top and the DIPC App below or
have the two side by side.
It is recommended to use two screens if possible.

![](images/200/image200_32.png)

## OR

![](images/200/image200_33.png)

22. Run Synchronize Data Task
    
    a. Click Save and Run
    ![](images/200/image200_34.png)
    
    b. A notification will appear that the job was saved.

    c. A new DIPC Job will be created to execute the task. A notification will appear in the notification bar as below:
    ![](images/200/image200_35.png)

    d. The job will automatically appear within the Jobs page. This may take up to 1 minute.
    ![](images/200/image200_36.png)

    e. Click on the Job to see the Job Details
    ![](images/200/image200_37.png)

    f. Auto-refresh is on, statuses will be updated frequently

    g. As the job executes, the Initial Load process is created in ODI while DIPC configures OGG for the Source Capture and Target Delivery

    h. As this job executes, the Replicated Sales OLTP Source Data table will be updated in the Demo Client. As new tables are created they will show up as yellow, when the row counts of the source and replicated schemas match the rows will turn green
    ![](images/200/image200_38.png)

Note: It may take several minutes for the Replicated Sales OLTP Data side to
show anything. This is normal.

    i. As the row counts of each table match the rows will turn green
![](images/200/image200_39.png)

    j. Optional: The Initial Load process (uses Data Pump) can also be monitored within ODI Console- (second created tab in Chrome) Expand Runtime/Sessions/Load Plan Executions then click on Sessions and on the glasses icon to view the status
    
![](images/200/image200_40.png)

    k. Optional: Click on the Session at the top of the list to view the Details in ODI Console
![](images/200/image200_41.png)

    l. Once the row counts match and the Initial Load process is complete the “Initial Load Complete” button within the Demo Client will be enabled.
![](images/200/image200_42.png)

    m. Go back to the Job Details in the DIPC App. to review the status there. The Initial load Action will show Successful after a little while (may take 7 minutes or more)
![](images/200/image200_43.png)

    n. Once done, the Initial load Action can be expanded to review the various steps underneath
![](images/200/image200_44.png)

    o. Click on Procedure:Initial load_PROC:DBLINK_DATAPUMP to review the Code generated by DIPC for the Initial Load. Click Done when you’ve completed the code review
![](images/200/image200_45.png)

# Task 3 : Validate DIPC data Synchronization Job

At this point DIPC has created and orchestrated the initial load and the data
synchronization process for the OLTP source and operational data store. A new DIPC
job is created and executed and can be monitored with the Jobs view.

1. You can also monitor the process by monitoring the DIPC Agent terminal
window. You could also monitor the DIPC Managed Server, however there is a
lot of detailed information here

2. Click Jobs and refresh until the newly created DIPC Job shows up.
    - You should see 5 Actions

3. The DIPC agent is orchestrating this process. Additional details can be seen in
the GG logs as well as within ODI Studio.

4. Before doing anything else monitor GG and watch for extracts and replicats to
be created and started and RUNNING

- Open Terminal on DIPC host machine
- cd /home/DIPC
- Execute ./GGINFO_ALL.sh
- Ensure both Extract and Replicat are running
![](images/200/image200_46.png)

5. Once all rows are green in the Demo Client, proceed to next step

![](images/200/image200_47.png)

# Task 4 : Monitor Source Inserts/Updates/Deletes

1. Now that the initial load is complete and the extract/replicat have been created
and are running, we can simulate insert/updates and deletes on the source and
monitor the replicated data through the Demo Client.

2. Using the Demo Client click on the “Initial Load Complete” Button (if you have NOT done it already).
![](images/200/image200_48.png)

3. The following screen will appear. NOTE – the current refresh of the client is 10
seconds.
![](images/200/image200_49.png)

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

![](images/200/image200_50.png)

5. This row will be automatically update on the replicated schema as the DIPC Job
picks up the change. The Demo Client is set to refresh at 10 seconds, so it will
at least take 10 seconds for the replicated table grid to update. Once the Demo
Client finds the change both rows will be updated to yellow.

![](images/200/image200_51.png)

6. The yellow highlights will automatically expire within the client.

7. To perform an insert click on the “Simulate Inserts” Button once.
This will perform an insert and the demo client will scroll to the row that was
inserted.

![](images/200/image200_52.png)

8. Depending on the refresh, the row may directly be replicated to the replicated
schema or appear in the next refresh by the Demo Client.

9. Both rows should show as yellow

10. To perform a delete click last row and click on the icon
 ![](images/200/image200_53.png) 
 
- Notice this record will be deleted from the replicated schema as well.

![](images/200/image200_54.png)

# Summary

You have now successfully completed the Hands on Lab, and have successfully performed an end-to-end data synchronization task through Oracle’s Data Integration Platform Cloud.

