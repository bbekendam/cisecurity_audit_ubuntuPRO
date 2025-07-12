# cisecurity_audit_ubuntu24_EC2

A hands on demonstration of executing a CISecurity Benchmark for Ubuntu 24 on an Brand New AWS EC2 host

Purpose:  To prove out assessment benchmark tools and identify vulnerabilities/weaknesses in hosts deployed in a default fashion.

<img width="790" height="607" alt="CISecurity Architecture" src="https://github.com/user-attachments/assets/1e911434-4522-48ad-b4a4-0345d10be4ad" />


_Assumptions - you have a valid AWS account (free tier available), and an Ubuntu Pro subscription (free for 5 hosts)_
1.  Create the EC2 Instance 
2.  Login to the EC2 instance via SSH
3.  Execute the commands to add the correct repositories
4.  Update the system connections and attach Ubuntu pro as needed
5.  Run the command to perform the assesment
6.  SCP the report back to local workstation
7.  Access the report and view the content
8.  Prompt and Use ChatGPT for Augmented Analysis with Remediation Guidance/Scripts

https://ubuntu.com/security/certifications/docs/usg/cis/audit <br>
https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final


---------------------------------------------------------------------------------------------

1.  Create the EC2 Instance (and keypair if necessary for access)
https://aws.amazon.com/free/compute/


<img width="993" height="945" alt="Screenshot 2025-07-11 at 4 38 39 PM" src="https://github.com/user-attachments/assets/3fc73f67-209e-4b1e-b6c3-89913fe3463c" />


<img width="999" height="942" alt="Screenshot 2025-07-11 at 4 41 07 PM" src="https://github.com/user-attachments/assets/fb1a2efa-314b-45fc-8cf4-18b6ba601af6" />

<br><br>

2.  Login to the EC2 instance via SSH
   
<img width="1051" height="604" alt="image" src="https://github.com/user-attachments/assets/58dcb19a-ec65-476a-993a-04a5e9e19bf9" />


<img width="833" height="602" alt="image" src="https://github.com/user-attachments/assets/7494a13d-8de5-4d44-afd3-3caa0c00f211" />


<br><br>
3.  Execute the commands to add the correct repositories


<img width="623" height="199" alt="image" src="https://github.com/user-attachments/assets/b7ad8827-aefa-4c4b-a258-20250b4504dc" />

<br><br>
4.  Update the system connections and attach Ubuntu pro as needed

<img width="2682" height="1490" alt="image" src="https://github.com/user-attachments/assets/8b6a82f0-d564-437c-a191-204e4d0378d2" />

<img width="650" height="414" alt="image" src="https://github.com/user-attachments/assets/5ebf9967-53c8-4ca0-92f4-bbdf586748a5" />

<img width="499" height="113" alt="image" src="https://github.com/user-attachments/assets/cb5de8e0-daff-4b18-9486-d977a371b378" />

<br><br>
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
<br>
XML and HTML files available
<br>

8.  Prompt and Use ChatGPT for Augmented Analysis with Remediation Guidance/Scripts
<br>
<br>

<img width="662" height="785" alt="image" src="https://github.com/user-attachments/assets/751fda24-a419-4f56-9cdb-a061b545c051" />
<br>
<img width="703" height="854" alt="image" src="https://github.com/user-attachments/assets/4c3298a7-7698-4c5c-8ebb-344d3ee6ba8f" />
<br>
<img width="766" height="834" alt="image" src="https://github.com/user-attachments/assets/e76694ad-5bf1-44ae-ba25-9249e70890ee" />
<br>
<img width="732" height="244" alt="image" src="https://github.com/user-attachments/assets/daf0dab4-7e24-4eae-ad35-71c99b53c25b" />
<br>

```
#!/bin/bash

echo "Starting CIS High Severity Remediation..."

# 1. Disable empty password logins
echo "Disabling login for accounts with empty passwords..."
passwd -l $(awk -F: '($2==""){print $1}' /etc/shadow)

# 2. Configure pam_faillock
echo "Configuring pam_faillock for failed login attempts..."

# Backup PAM config
cp /etc/pam.d/common-auth /etc/pam.d/common-auth.bak_$(date +%F-%T)
cp /etc/security/faillock.conf /etc/security/faillock.conf.bak_$(date +%F-%T) 2>/dev/null

# Append faillock config if not present
if ! grep -q "auth required pam_faillock.so preauth audit silent deny=5 unlock_time=900" /etc/pam.d/common-auth; then
  sed -i '/^auth.*pam_unix.so/a auth required pam_faillock.so preauth audit silent deny=5 unlock_time=900' /etc/pam.d/common-auth
fi

if ! grep -q "auth \[default=die\] pam_faillock.so authfail audit deny=5 unlock_time=900" /etc/pam.d/common-auth; then
  sed -i '/^auth.*pam_unix.so/a auth [default=die] pam_faillock.so authfail audit deny=5 unlock_time=900' /etc/pam.d/common-auth
fi

if ! grep -q "account required pam_faillock.so" /etc/pam.d/common-auth; then
  sed -i '/^account.*pam_unix.so/a account required pam_faillock.so' /etc/pam.d/common-auth
fi

# 3. Ensure system accounts do not use /bin/sh (Commented; audit first)
# echo "Checking system accounts for /bin/sh shell (this is a placeholder)..."
# awk -F: '($3 < 1000 && $7 == "/bin/sh") {print $1 " is using /bin/sh"}' /etc/passwd

echo "CIS High Severity Remediation Complete."
```


<br><br>

<img width="490" height="184" alt="image" src="https://github.com/user-attachments/assets/d0cfc7d7-37eb-4fcc-81e0-00845257ea23" />



