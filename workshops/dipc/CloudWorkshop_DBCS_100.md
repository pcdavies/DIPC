# Create a Data Integration Platform

# Cloud Instance

## Before You Begin

```
This tutorial shows you how to create a Data Integration Platform
Cloud instance and it takes approximately 30 minutes to complete.
These 30 minutes don't include waiting times for instances to be
created. (And there are a lot of screenshots here, otherwise, the
tutorial is not that long.)
```
## Background

```
Data Integration Platform Cloud (DIPC) is an Oracle cloud service that
offers a single platform to connect to hundreds of on-premises and
cloud data sources. From this platform you extract, load and transform
(ELT) data entities of any shape and format, synchronize or replicate
selected data sources, integrate with big data technologies, perform
data analytics and maintain data quality.
```
```
When you create an Oracle Data Integration Platform Cloud service
instance, you create a Data Integration environment in the cloud. Data
integration applications are installed for you on one or more VMs
which offer you consoles to perform all your data integration needs.
```
```
For Data Integration Platform Cloud, you can select one of the
following editions:
```
```
■ Standard Edition: For a bulk copy of your data sources to the
cloud, or to extract, load and transform your data.
■ Enterprise Edition: For a selective copy or real time replication of
your data sources, or to extract, load and transform your data.
■ Governance Edition: To extract, load, transform, manage,
replicate, and maintain data quality.
```
```
For this tutorial, you create an instance with Enterprise Edition.
```
## What Do You Need?

```
■ The link, username and password to My Services page for your
Oracle cloud services. (When you request for Oracle cloud
services, you get an email with this information.)
■ A web browser
```

## Find Your Services and Backup

## Location

```
1. In your web browser, paste the link you received in email for Oracle
cloud's My Services page.
2. Enter your user name and password, then click Sign In. (You'll
need to reset your password, if it's your first time visiting this page.)
```
```
Description of the illustration 001.002.png
```
```
3. If it's your first time, you'll get tile options for the Guided Journey.
For this tutorial, instead of the Guided Journey experience, click
Dashboard. (And later, experience the tiles on your own.)
```

```
Description of the illustration 001.003.png
```
4. Click Customize Dashboard and then click Show for the following
three services:
■ Infrastructure> Storage Classic
■ Data Management > Database (If there's an existing database
deployment, then this tile will already be in the Services section.)
■ Integration > Data Integration Platform Cloud

5. Confirm that these three services appear as three tiles on your
dashboard.


```
Description of the illustration 001.005.png
```
6. Click the action menu of the Storage Classic tile and then click
View Details.

```
Description of the illustration 001.006.png
```
7. In the Additional Information section, copy the URL displayed in
the REST Endpoint field and paste it into a notepad, ready for the
other sections which require the Storage Container information.
Example for REST Endpoint URL: https://<your


```
domain>.us.storage.oraclecloud.com/v1/Storage-
<your domain>
```
```
Description of the illustration 001.007.png
```
8. Click Open Service Console.

```
Description of the illustration 001.008.png
```
9. A replication policy defines your primary data center (dc) and
whether your data should be replicated to a geographically distant
(secondary) data center. If it's your first time, then you'll get a Set a
Georeplication Policy before Continuing dialog box. Read the
instructions, consult with the Storage Classic administrator or your
account administrator, select a policy from the drop-down menu
and click Set Policy. You'll only have to set this policy once and
you can't change it later. If your policy is already set, then go to the
next section Learn more.


```
Description of the illustration 001.009.png
```
10. Click the offscreen toggle menu (displayed as a hamburger icon)
and then click My Services to go back to the list of services.

## Create a Database Deployment

```
1. In the Dashboard, locate Database in the list of services. (Use
Customize Dashboard to make your three services re-appear if
they are not displayed. Refer to step 1-4.) From its Action Menu
select Open Service Console.
```

```
Description of the illustration 002.001.png
```
2. In case you get a welcome page, click Go to Console.

3. In the Instances page, click Create Instance.

4. Complete the Instance page as follows: (You may have less fields
due to your subscription type.)
■ Service Name: DBCSDEF
■ Description: DEF database for DIPC
■ Notification Email: <a valid email address to receive
provisioning status>
■ Region: No Preference (If you select a region, then you'll get a
deployment on Oracle Cloud Infrastructure (OCI) and you can't
use it for the DIPC instance in the next section.)
■ Tags: warehouse (Click the Click to Create a Tag button,
create a tag called warehouse and then click OK.)
■ Bring Your Own License : de-select (You may not have this
option.)
■ Service Level: Oracle Database Cloud Service (You may not
have this option.)
■ Metering Frequency: Monthly (You won't have this option for
trial versions)
■ Software Release: Oracle Database 12c Release 1
■ Software Edition: Enterprise Edition
■ Database Type: Single Instance


```
Description of the illustration 002.004.png
```
5. Click Next and then on the Details page, complete the Database
Configuration fields as follows:
■ DB Name: ORCL
■ PDB Name: PDB
■ Administration Password and Confirm Password fields:
password
■ Usable Data Storage (GB): 25

```
The entry for Usable Database Storage, populates the
Total Data File Storage (GB) field to reflect the amount
of storage for your instance, such as space for
operating system and product binaries, supporting
files, database data and configuration files. After you
create the instance, you can add more data storage
later.
```
```
■ Total Data File Storage (GB): 88.
■ Compute Shape: OC3 - 1.0 OCPU, 7.5 GB RAM
■ Click Edit for SSH Public Key.
■ In the SSH Public Key for VM Access dialog, select Create a
New Key, then click Enter.
```

```
Description of the illustration 002.005.png
```
■ Click Download in the Download Keys dialog box.

■ Save the sshkeybundle.zip file to your computer.

■ Confirm that the SSH Public Key field now contains a public key
value.


```
Description of the illustration 002.005c.png
```
6. Expand Advanced Settings, and then complete the fields as
follows:
■ Listener Port: 1521
■ Select your timezone from the Timezone menu.
■ Select Enable Oracle GoldenGate.
■ De-select Include "Demos" PDB to save database space.

```
Description of the illustration 002.006.png
```

7. Complete the Backup and Recovery Configuration fields as
follows, and then click Next:
■ Backup Destination: Both Cloud Storage and Local Storage
■ Cloud Storage Container: Enter the URL of a new or existing
container in the format of the REST Endpoint URL you found in
step 2-6 and append it with a slash and then the container name.
If you want a new container created for you, you append a new
name, instead of an existing container name, and then select the
checkbox to create the container. (For this tutorial, there are no
existing containers, so you should create a new one.)
Format: rest_endpoint_url/containerName
Example: https://dipc.storage.oraclecloud.com/v1/S
dipc/dbcsDEF

```
The Cloud Storage Container field is prepopulated with
your cloud storage REST endpoint information,
appended with a new container named DBaaS in the
format of
https://dipc.storage.oraclecloud.com/v1/S
dipc/DBaaS. Change this container to a name that
can be identified with this database instance. For this
tutorial, it is dbcsDEF.
.https://dipc.storage.oraclecloud.com/v1/
dipc/dbcsDEF
```
```
■ Username: Enter the username for My Services which applies to
Storage Classic, Database and Data Integration Platform Cloud.
If you don't know it, refer to the What Do You Need section of
this tutorial.
■ Password: Enter the password for My Services. Use your latest
password. If you don't know it, refer to the What Do You Need
section of this tutorial.
```

```
Description of the illustration 002.007.png
```
```
8. Click Next and ensure that in the Confirm step, you get a message
that the container was created.
```
```
Description of the illustration 002.008.png
```
```
9. Review the details for your database cloud deployment. If you need
to make changes, click Previous or use the navigation train to go
back. Otherwise, click Create.
```
10. Click the DBCSDEF instance and refresh the Service Overview
page until the status displays Ready.


```
Description of the illustration 002.010.png
```
## Create a Data Integration

## Platform Cloud Instance

```
1. Locate Data Integration Platform Cloud in My Services
dashboard and, then select Open Service Console from
the Actions menu.
```
Before You Begin

Find Your Services and
Backup Location

Create a Database
Deployment

Create a Data Integration
Platform Cloud Instance

```
Want to Learn More?
```

```
Description of the illustration 003.001.png
```
2. If you get a welcome page, click Go to Console.

3. In the Instances page, click Create Instance.

4. Complete the Instance fields as follows:

```
■ Service Name: DIPCDEF
■ Service Description: Data Integration Platform
Cloud for DEF instance
■ Notification Email:<a valid email address to receive
provisioning status>
■ Tags: DEF (Click the plus symbol to create a tag called DEF )
■ Cluster Size: 2
■ Service Edition: Governance Edition (Refer to Before you
Begin section of this tutorial to learn more about these editions.)
```

```
Description of the illustration 003.004.png
```
5. Complete the Database Configuration fields as follows: (This
database is used to store the schema of the Data Integration
Platform Cloud server for this instance.)
■ Database Service: DBCSDEF (You'll have the database
deployment from section 2 of this tutorial in the drop-down menu,
if your database was created on OCI classic, is currently running
and it is in the same domain (same My Services page) as this
Data Integration Platform Cloud instance.)
■ PDB Name: PDB
■ Username: SYS
■ Password: password

```
Description of the illustration 003.005.png
```
6. Complete the Backup and Recovery Configuration fields as
follows:


```
■ Cloud Storage Container: The container field is automatically
filled with the proper container URL format. This format is the
REST Endpoint URL you found in step 1-7, appended with a
slash and then the container name. If you want a new container
created for you, just append a new name, instead of an existing
container name, and then select the checkbox to create a
container.
Format: rest_endpoint_url/containerName
Example: https://dipc.storage.oraclecloud.com/v1/S
dipc/dipcDEF
■ Cloud Storage Username: Enter the username for My Services
which applies to Storage Classic, Database and Data Integration
Platform Cloud. If you don't know it, refer to the What Do You
Need section of this tutorial.
■ Cloud Storage Password: Enter the password for My Services.
Use your latest password. If you don't know it, refer to the What
Do You Need section of this tutorial.
■ Create Cloud Storage Container: select checkbox
```
```
Description of the illustration 003.006.png
```
7. Complete the WebLogic Server Configuration fields as follows:

```
■ Compute Shape: OC3m - 4.0 OCPU, 60.0 GB RAM
■ Click Edit for SSH Public Key.
■ Separately, in your computer's file browser, find the zipped folder
containing the system generated key for the database
deployment, called sshkeybundle.zip and unzip it. (Refer to
section 2-5 of this tutorial. You can also create a new key for this
section.)
■ In the SSH Public Key for VM Access dialog box, select Key
File Name and then browse to sshkeybundle folder and select
publicKey. Then click Enter.
```

```
Description of the illustration 003.007a.png
```
■ Administrator Username: <Your choice of username to
access consoles of Data Integration Platform
Cloud>

■ Password: <Your choice of password for the
username in this section>

■ Confirm Password: <Confirm your choice of password
for the username in this section>


```
Description of the illustration 003.007b.png
```
```
8. Click Next.
9. Review the details for your Data Integration Platform Cloud
instance. If you need to make changes, click Previous or use the
navigation train to go back. Otherwise, click Create.
```
10. In the Instances page, confirm that the DIPCDEF instance appears
in the list of instances with the Status displayed as: Creating
service....

```
Description of the illustration 003.010.png
```
```
11. Refresh the Instances page until the Status: Creating service ...
is no longer displayed on this page.
```
12. Click the DIPCDEF instance to go to the Instance Overview page.


About Oracle Contact Us Legal Notices Terms of Use Your Privacy Rights Copyright © 2018, Oracle and/or its affiliates. All rights
reserved.

```
13. Confirm that the Status field displays Ready.
14. Go back to the Instances page.
15. Click the Action Menu of DIPCDEF and then click Data
Integration Platform Console to access this console.
```
## Want to Learn More?

```
■ Data Integration Platform Cloud on Oracle Help Center
■ Data Integration Platform Cloud on Oracle Cloud Website
■ Oracle Database Cloud on Oracle Help Center
```

