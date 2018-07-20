# Appendix1: SSH Session Configuration

## Create SSH Configuration

1.	Start PuTTY

![](images/Ap1/imageAp1_10.png)
 

2.	In the screen provide the following information:
-  Host: **<SERVER_IP_ADDRESS>**
- Saved Session: Provide a name 

![](images/Ap1/imageAp1_20.png)
 
3.	Click on “Save” button
4.	From the hierarchical panel on the left, select “Connection > Data” and provide the following information:
- Auto-login username: opc

![](images/Ap1/imageAp1_30.png)

5.	From the hierarchical panel on the left, select “Connection > SSH > Auth”. Click on “Browse”  button to select the private key file

 ![](images/Ap1/imageAp1_40.png)

6.	Navigate to the directory in which you copied the files provided for the labs and select “dipcdemoSSH.ppk”. Click on “Open” button

 ![](images/Ap1/imageAp1_50.png)

7.	From the hierarchical panel on the left, select “Connection > SSH > Tunnels” and provide the following information:
- Source port: 6905
- Destination: **<SERVER_IP_ADDRESS>**:5901
8.	Click on “Add” button

 ![](images/Ap1/imageAp1_60.png)

9.	From the hierarchical panel on the left, select “Sessions” (on top) and then click on “Save” button. This will save this configuration so you can re-use it.

 ![](images/Ap1/imageAp1_70.png)

10.	Click on “Open” button to start your SSH session. If you are asked for a passphrase, provide “dipc”

 ![](images/Ap1/imageAp1_80.png)




## Load Existing Configuration
If you have saved the SSH configuration previously.

1.	Start PuTTY

![](images/Ap1/imageAp1_10.png)

2.	Select your configuration in the “Saved Sessions” section then click on “Load” button

 ![](images/Ap1/imageAp1_90.png)

3.	Click on “Open” button to start your SSH session. If you are asked for a passphrase, provide “dipc”
 
![](images/Ap1/imageAp1_100.png) 
