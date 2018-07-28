# Lab 100 -  Creating a Data Integration Platform Cloud Instance
![](images/100/image100_0.png)


## Before You Begin

### Objectives
- Review steps to provision a Database Cloud Service to be used for DIPC
- Provision a Data Integration Cloud Service instance (DIPC).

### Time to Complete
Approximately 30 minutes, not including wait time for service activations.

### What Do You Need?
Your will need:
- Oracle Cloud URL
- Oracle Cloud User and Password
- General understanding of RDBMS and data integration concepts


## Logging Into Oracle Cloud Instance

1. In your web browser, navigate to cloud.oracle.com, then click Sign in.
2. Provide the cloud account: oscnas001 then <Enter>
3. Provide your user name and password, then click Sign In.

![](images/100/image100_1.png)

Click Services or Go to Dashboard to access My Oracle Services.

## Creating an Oracle Database Cloud Instance

1. Locate Database in your list of services, then select "Open Service Console" from the Action menu.

![](images/100/image100_2.png)

2. On the Services page, click "Create Instance" button. This launches the Create DBC instance wizard.

![](images/100/image100_3.png)

3. Complete the Service form as follows and then click "Next" button:
    -  Instance Name: DBCSABC
    - Description: ABC Replication Database for Data Integration Platform Cloud
    - Notification Email: (a valid email address to receive provisioning status)
    - Region: No Preference
    - Software Release: Oracle Database 12c Release 1
    - Software Edition: Enterprise Edition
    - Database Type: Single Instance

![](images/100/image100_4.png)

4. On the Service Details page, complete the Database Configuration fields as follows:

    - DB Name (SID): ORCL
    - Pluggable Database (PDB) name: PDB1
    - Administration Password and Confirm Password fields: Welcome_123#
    - Usable Database Storage: 25
    - Total Data File Storage (GB) - Based on your entry of the previous field ( Usable Database Storage), this field will be updated to reflect the amount of storage that will be allocated to your instance; including space for operating system and product binaries, supporting files, database data and configuration files, and so on. After you create the service instance, you can add more data storage as needed. 
    - Compute Shape: OC4
    - Click Edit for SSH Public Key.

    In the SSH Public Key for VM Access dialog, select Create a New Key, then click Enter.

    ![](images/100/image100_5.png)

    Click Download in the Download Keys dialog box.

    ![](images/100/image100_6.png)

    Save the sshkeybundle.zip file to your computer.

    ![](images/100/image100_7.png)

    Confirm that the SSH Public Key field now contains a public key value.

![](images/100/image100_8.png)

5. Expand Advanced Settings, and then complete the fields as follows:
    - Listener Port: 1521
    - Select your timezone from the Timezone menu.
    - Select "Enable Oracle GoldenGate".
    - Deselect "Include 'Demos' PDB" to save database space.

![](images/100/image100_9.png)

6. Complete the Backup and Recovery Configuration fields as follows, and then click "Next" button:
    - Backup Destination: Both Cloud Storage and Local Storage
    - Cloud Storage Container: Enter the name of your storage container in the format, Storage-**\<identity domain name>**/**\<container name>**. For example: https://oscnas001.us.storage.oraclecloud.com/v1/Storage-oscnas001/dbcs-TT.
    - Username: Enter your username for Oracle Storage Cloud
    - Password: Enter your password for Oracle Storage Cloud
    - Select "Create Cloud Storage Container" to create a new container.

![](images/100/image100_10.png)

7. Review the Service Details for your DBCS instance. If you need to make changes, click "Previous" or use the navigation train to go back. Otherwise, click **"CANCEL". Please DO NOT Create!**, the instance creation process can take some time; that is why we have already created the instances in advance. Proceeed to the next section.

## Creating an Oracle Data Integration Platform Cloud Instance

In this section, you create an Oracle Data Integration Platform Cloud instance using the instance creation wizard.

1. Locate Data Integration Platform Cloud in your list of services, then select Open Service Console from the Options menu.

![](images/100/image100_11.png)

2. In the Services page, click "Create Instance".

![](images/100/image100_12.png)

3. Complete the Service fields as follows, and hen click "Next" button:
    - Service Name: DIPCABC
    - Description: Data Integration Platform Cloud for ABC instance
    - Email Address: (a valid email address to receive provisioning status)
    - Cluster Size: 2
    - Service Edition: Governance Edition

![](images/100/image100_13.png)

4. Complete the Database Configuration fields as follows:

    - Oracle Database Cloud Service Instance Name: DBCSABC
    - PDB Name: PDB1
    - Administration Username: SYS
    - Password: Welcome_123#

![](images/100/image100_14.png)

5. Complete the Backup and Recovery Configuration fields as follows:

    - Cloud Storage Container: Storage-dipc/dipcABC
    - Cloud Storage User Name: Enter your username for Oracle Storage Cloud
    - Cloud Storage Password: Enter your password for Oracle Storage Cloud

![](images/100/image100_15.png)

6. Complete the Weblogic fields as follows:

    - Compute Shape: OC3m - 4.0 OCPU, 60.0GB RAM
    - SSH Public Key:
        
        a. Click Edit.
        
        b. In the SSH Public Key for VM Access dialog, select Create a New Key and then click Enter.

        c. In the Download Keys dialog, click Download and save your  "SSHkeybundle.zip" to your local machine.

    - Administrator Username: weblogic
    - Admin Password: Enter the admin password that you'll use later to login to all the consoles for this service instance, with the correspondent username you have had specified. For example welcome1
    - Confirm Admin Password: Reenter the admin password

![](images/100/image100_16.png)

7. Click "Next" button and review your Data Integration Platform Cloud instance configuration details. If you need to make any changes, click "Previous" or use the navigation train to go back. Otherwise, click **"CANCEL". Please DO NOT Create!**, the instance creation process would normally take up to 30 minutes, so we have already created the instance in advance for the workshop.


## Summary
You have now successfully completed the Hands-on Lab, and reviewed the requirements and necessary steps to provision a Data Integration Platform Cloud (DIPC) instance.