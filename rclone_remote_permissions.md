
### **MANUAL DIAGNOSTIC FOR CHECKING PERMISSIONS ON A RCLONE REMOTE**

If you are getting error messages related to reading/accessing your rclone remotes then run the following commands:

1. Check that the source and destination remotes exist and are configured correctly in rclone.conf
  - `rclone config show remote`
  - ^^ Use remote name without colon `:`
  - ^^ Check that all of the fields in your remote look correct. A TD has a teamdrive ID. SA or id/secret auth is present

2. Check that you can read files on the remote. Feel free to use ls or lsf rather than rclone lsd.
  - `rclone lsd remote:`
  - `rclone lsd remote: --drive-service-account-file=/opt/sa/NUMBER.json`
  - ^^ Run this command using both the MIN and MAX json numbers in your json folder to ensure all of your SAs/jsons have read permission
  - ^^ Double check that sasync.conf is pointing to the location where your folder jsons sit
  - ^^ Run the above command using both the remote: name and the remote:folder name specified in your set file ```

3. Check that you can write and delete to the root of the remote using your default remote config
  - `rclone touch remote:test123.txt`
  - ^^ Check that the file is present on your remote
  - `rclone deletefile remote:test123.txt`
  - ^^ Check that the file has now been deleted from your remote
  - As an extra check you can run the above commands writing/deleting to remote:folder/folder2 specified in your set.file

4. Check that you can write and delete to the root of the remote using service accounts
  - `rclone touch remote:test123.txt --drive-service-account-file=/opt/sa/NUMBER.json`
  -  Replace NUMBER with a json file number
  - ^^ Check that the file is present on your remote
  - `rclone deletefile remote:test123.txt --drive-service-account-file=/opt/sa/NUMBER.json`
  - ^^ Check that the file has now been deleted from your remote
  - As an extra check you can run the above commands writing/deleting to remote:folder/folder2 specified in your set.file

### **IF USING SASYNC...**

5. Enable rclone remote checks in sasync
  - In sasync.conf ensure that CHECK_REMOTES=true

