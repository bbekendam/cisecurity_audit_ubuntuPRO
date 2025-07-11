# cisecurity_audit_ubuntu24_EC2

A hands on demonstration of executing a CISecurity Benchmark for Ubuntu 24 on an AWS EC2 host
_Assumptions - you have a valid AWS account (free tier available), and an Ubuntu Pro subscription (free for 5 hosts)_


1.  Create the EC2 Instance (and keypair if necessary for access)
https://aws.amazon.com/free/compute/


<img width="993" height="945" alt="Screenshot 2025-07-11 at 4 38 39 PM" src="https://github.com/user-attachments/assets/3fc73f67-209e-4b1e-b6c3-89913fe3463c" />


<img width="999" height="942" alt="Screenshot 2025-07-11 at 4 41 07 PM" src="https://github.com/user-attachments/assets/fb1a2efa-314b-45fc-8cf4-18b6ba601af6" />



3.  Login to the EC2 instance via SSH
   
<img width="1051" height="604" alt="image" src="https://github.com/user-attachments/assets/58dcb19a-ec65-476a-993a-04a5e9e19bf9" />


<img width="833" height="602" alt="image" src="https://github.com/user-attachments/assets/7494a13d-8de5-4d44-afd3-3caa0c00f211" />



3.  Execute the commands to add the correct repositories


<img width="623" height="199" alt="image" src="https://github.com/user-attachments/assets/b7ad8827-aefa-4c4b-a258-20250b4504dc" />


4.  Update the system connections and attach Ubuntu pro as needed

<img width="2682" height="1490" alt="image" src="https://github.com/user-attachments/assets/8b6a82f0-d564-437c-a191-204e4d0378d2" />

<img width="650" height="414" alt="image" src="https://github.com/user-attachments/assets/5ebf9967-53c8-4ca0-92f4-bbdf586748a5" />

<img width="499" height="113" alt="image" src="https://github.com/user-attachments/assets/cb5de8e0-daff-4b18-9486-d977a371b378" />


5.  Run the command to perform the assesment


Initially we see the options and profiles available.  Choose ubuntu server EC2 level 1
<img width="688" height="299" alt="image" src="https://github.com/user-attachments/assets/3d33307e-e0bc-4c8b-ad8c-aece2b00fb20" />


```
usg audit cis_level1_server_ec2
```
<img width="1038" height="792" alt="image" src="https://github.com/user-attachments/assets/fca5ee40-6174-4c56-9708-6b97018f763d" />


<img width="1024" height="656" alt="image" src="https://github.com/user-attachments/assets/aca501f7-bac9-4819-a86a-c59757b1996d" />


6.  SCP the report back to local workstation

A quick copy over to the /tmp directory

<img width="1182" height="296" alt="image" src="https://github.com/user-attachments/assets/875953a6-f117-4374-803d-5f7aee822822" />

Yet access denied

<img width="2530" height="64" alt="image" src="https://github.com/user-attachments/assets/bafc6599-19c3-43a7-955c-643019a229cc" />

Reminder to change the permissions to allow for basic user read (chmod 644)

<img width="796" height="233" alt="image" src="https://github.com/user-attachments/assets/f6ff40d3-6faf-49af-902b-2a5f08d8d342" />

Grants read access

<img width="2524" height="68" alt="image" src="https://github.com/user-attachments/assets/c0263d52-f2ac-45c1-9344-a0a68bb333b4" />


7.  Access the report and view the content

General Overview and Full Details

<img width="867" height="1006" alt="image" src="https://github.com/user-attachments/assets/dfe326ee-b884-446d-83f2-3d1da6f3ee28" />

Report Pivots to NIST 800-53 Compliance
https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final

<img width="912" height="1008" alt="image" src="https://github.com/user-attachments/assets/256236c9-47a5-4e13-9f12-b2a3b31d6321" />

XML and HTML files available


