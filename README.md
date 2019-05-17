# sa-guide : Guide to creating service accounts and using them with rclone copy/sync

Multiple service accounts (SAs) along with a rotation script such as sasync can be useful when you need to sync or copy large amounts of data up to or between google drive accounts. The daily limit for uploads using a single gsuite account is 750GB. Each service account has its own quota. So 10 service accounts will have a combined upload quota of 7.5TB (10 x 750GB). Below is a guide and some tools to help you get it all working.

[1. Setup - This guide](https://github.com/88lex/sa-guide)

Tools:

[2. sa-gen - Creating Service Accounts](https://github.com/88lex/sa-gen)

[3. sasync - Creating and running rclone sync with sets](https://github.com/88lex/sasync)

[4. checkrcmount - Check rclone mounts](https://github.com/88lex/checkrcmount)

[5. cleanremotes - Clean rclone remotes](https://github.com/88lex/cleanremotes)

**************
**NOTE:** If you want to use [sa-gen](https://github.com/88lex/sa-gen) and [sasync](https://github.com/88lex/sasync) please take the time to read the document below along with readme instructions that we've written for the repos. Also read through the scripts a couple of times. The scripts are all pretty straightforward. 

The scripts and methods are based on ideas/contributions/tools from ncw, zenjabba, max, sk, rxwatcher, dashlt, mc2squared, storm, physk and others.

I wanted to share this but I don't have a lot of time for support. If you can try to help others on discord/slack channels after figuring out the steps that would be great. All of the scripts do work, but require some very basic knowledge for running bash scripts, setting permissions (e.g. chmod +x to run scripts in bash) and ensuring that your scripts are pointing to files/folders in the correct locations (e.g. /opt/sa for json keys, /opt/sasync/json.count for the sasync counter, etc.).
********


1. Create one or more Google Projects. You need projects to create service accounts.
Each project can have up to 100 service accounts. Each service account has a quota of 750GB upload/day and 10TB download/day. Instructions to create a project are here:  https://cloud.google.com/resource-manager/docs/creating-managing-projects
You can name the project as you like. A simple description is often best. For example we use “sasync01”, “sasync02” and so on which reminds us that the project is being used for service account syncing.

2. Enable Identity Access Management (IAM) API.
Go to this page and choose a project that you have created (drop down near the top).
	https://console.developers.google.com/apis/library/iam.googleapis.com
	Click “Enable”

3. Enable Google Drive API.
	Go to this page and choose a project that you have created (drop down near the top).
https://console.developers.google.com/apis/library/drive.googleapis.com
	Click “Enable”

4. Create Google service accounts manually or with a script.  
.  
MANUAL: To create service accounts manually follow these instructions. Be sure to download every service account key as a .json file as you will need them later in order to use SAs with rclone.  
	https://support.google.com/a/answer/7378726?hl=en  
	https://console.cloud.google.com/iam-admin/serviceaccounts/create  
If you intend to use an automated script to sync or copy files then rename the service account json files to 1.json, 2.json and so on. Otherwise the script will not work without modification.  
.  
USING A SCRIPT:  
There are a few scripts floating around to create 100 service accounts for each google project. Most rely on gcloud sdk or python. Here are a few, but always good to search for others.  
Gcloud SDK scripts:  
Here is one that I modified from scripts created by DashLt and mc2squared  
https://github.com/88lex/sa-gen  
These are the originals:  
https://gist.github.com/DashLt/4c6ff6e9bde4e9bc4a9ed7066c4efba4  
https://gist.github.com/mc2squared/01c933a8172a26af88285610a0e5af8d  
This is a Python script from zenjabba with instructions from Max:  
https://docs.google.com/document/d/1I3s53eC3cl3u6xBHvoW9cKbxoYowZU0JwavCFl-bSY0/edit?usp=sharing  
(if the repo linked in the instructions above is not available you can use this repo instead https://github.com/88lex/create_service_accounts-master )

5. Create a Google Group.
Go to groups.google.com and create a group.

6. Add your service accounts to a Google group.
You can add service accounts to a group manually or in bulk.
.  
MANUAL: From groups.google.com choose the group you want to use. Choose ‘Manage Members’ on the right, then choose ‘Direct add members’ on the left. Enter the service account email addresses you wish to add.
.  
BULK: Go to this link https://admin.google.com/ac/groups . Choose your group name. Click the Members section. Hover over the yellow + sign and choose Bulk Add. The pop up will explain how to download a csv template to add your service account IDs and then re-upload the csv to the group.

7. Add the google group to your source and destination Team Drives and/or My Drive folders.
Team Drives: Right click the Team Drive, choose Add Members and add the Group email. Give Manager or Content Manager permission to the Group.
My Drive: Right click the folder in My Drive, click Share then add the Group email.

8. Configure sasync or other script to copy/sync files to shared TDs/folders using your service accounts.
Sasync:  https://github.com/88lex/sasync
Instructions in the Readme on github.

