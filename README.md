
# <div align="center"> sa-guide 
**Instructions to create service accounts and use them with rclone.**</div>

### Do I need service accounts?   
  - In most cases, no. The upload, download and api quotas for Google accounts are sufficient for most users. Quotas are 750GB upload, 10TB download per day.
  - If you plan to upload, copy or sync > 750Gb in a day then you might want to set up and use service accounts.
  - For example 10 service accounts will have a combined upload quota of 7.5TB  (10 x 750GB). 

### Below is a guide and some tools to help you get it all working.

### [1. Setup - This guide](https://github.com/88lex/sa-guide)

### [2. sa-gen - Creating Service Accounts](https://github.com/88lex/sa-gen)

### [3. Manual diagnostic for checking permissions of rclone remotes with SAs and drives](https://github.com/88lex/sa-guide/blob/master/rclone_remote_permissions.md)

### [4. sasync - Creating and running rclone sync with sets](https://github.com/88lex/sasync)

### [5. checkrcmount - Check rclone remotes are accessible](https://github.com/88lex/checkrcmount)

### [6. cleanremotes - Clean rclone remotes](https://github.com/88lex/cleanremotes)

### [7. mountsize - Check the size and file count of configured rclone remotes](https://github.com/88lex/mountsize)

### [8. diffmove/diffsets - Check source vs destination differential files to the destination](https://github.com/88lex/diffmove)

**************
**NOTE:** Please take the time to read the document below and any readme in the repos. The scripts require a basic knowledge of bash, setting variables and permissions (e.g. chmod +x to run scripts in bash).
********

1. **Create a Google Group**.
Go to groups.google.com and create a group. You can also use an existing group.

2. **Create Google service accounts with the sa-gen script**.  https://github.com/88lex/sa-gen  

3. **Add your service accounts to a Google group**. 
You can add service accounts to a group manually or in bulk.    
  
MANUAL: From groups.google.com choose the group you want to use. Choose ‘Manage Members’ on the right, then choose ‘Direct add members’ on the left. Enter the service account email addresses you wish to add.    
  
BULK: Go to this link https://admin.google.com/ac/groups . Choose your group name. Click the Members section. Hover over the yellow + sign and choose Bulk Add. The pop up will explain how to download a csv template to add your service account IDs and then re-upload the csv to the group.
[ Find cli command to simplify? GAM will do but requires install. ]

4. **Add the google group** to your source and destination Team Drives and/or My Drive folders.    
Team Drives: Right click the Team Drive, choose Add Members and add the Group email. Give Manager or Content Manager permission to the Group.
. 
My Drive: Right click the folder in My Drive, click Share then add the Group email.

5. **Configure sasync or other script to copy/sync files** to shared TDs/folders using your service accounts.
Sasync:  https://github.com/88lex/sasync
sasync instructions are in the Readme.md on github.


********************************
********************************
CREDITS: The scripts and methods are based on ideas/code/tools from ncw, max, sk, rxwatcher, l3uddz, zenjabba, dashlt, mc2squared, storm, physk and others. If I forgot anyone no offense intended. Ping me and I'll add you.