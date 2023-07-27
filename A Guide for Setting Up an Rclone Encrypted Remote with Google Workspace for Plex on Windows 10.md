#### Setting up Rclone

1.  Download latest Rclone 64 Bit for Windows: [https://rclone.org/downloads/](https://rclone.org/downloads/)
2.  Unzip the folder to C:\rclone
3.  Open CMD (Admin) in rclone folder (or navigate using cd c:\rclone)
4.  Type rclone config
5.  Type n for New Remote
6.  Enter name for new remote. I use gdrive.
7.  Type 16 for Google Drive (Not Google Cloud Storage) (Double check number, might have changed)
8.  Now it is time to make your own client_id
9.  Go to [https://console.developers.google.com/](https://console.developers.google.com/)
10. Create a New Project

11. Under “ENABLE APIS AND SERVICES” search for “Drive”, and enable the “Google Drive API”

12. Click “Create credentials”, then “Help Me Choose”.

13. Select "Google Drive API"

14. Select "User data" then "Save and Continue"

15. Under OAuth Client ID, choose "Desktop App" under Application type

16. Press Done. When asked for client name use "oAuth 2.0 Client ID".

17. Go to Credentials tab on left and click on the oAuth 2.0 Client ID you just created to find the Client ID and Client secret.

18. Copy the Client ID

19. Go back to CMD and right click to paste the Client ID

20. Copy the Client Secret

21. Go back to CMD and right click to paste the Client Secret

22. You will now be prompted to choose a number for the scope – type 1 and then enter

23. You will now be prompted to either enter a string value for the root folder - I named mine "Backup"

24. You will now be prompted to enter a string value for the service_account_file - Leave this blank and press enter

25. Next you will be asked if you’d like to edit the advanced config (y/n) - Type n and then enter

26. Now you’ll be asked if you’d like to use auto config - Type y and then enter

27. You will now be taken to the sign-on page for Google Drive – if not, enter the following in your web browser [http://127.0.0.1:53682/auth](http://127.0.0.1:53682/auth)

28. Go back to CMD. You will be asked if you'd like to configure a Team Drive - Type n

29. Your finalized version of the config file will now be output in CMD - Type y to accept

30. The rclone config file has now been built and will be located in C:\Users\username\AppData\Roaming\rclone

31. Now let's create an encrypted remote to point at gdrive.

32. Type rclone config

33. Type n for new remote

34. Name the new remote gcrypt

35. Type crypt

36. Type gdrive:/crypt to add the encrypted folder "crypt" to your gdrive remote.

37. Type 1 to choose full filename encryption

38. Type 1 to choose full folder encryption

39. Type y to choose your own password

40. Choose a password, and enter twice for confirmation.

41. Choose a salt pass word, and enter twice for confirmation.

42. Press n to ignore advanced config

43. Press y to confirm remote config is correct

44. Press q to quit

#### Setting up Rclone Browser

1.  Download the latest 64 bit version of Rclone Browser: [https://github.com/kapitainsky/RcloneBrowser/releases](https://github.com/kapitainsky/RcloneBrowser/releases)
2.  Unzip the file in C:\rclone
3.  Open the RcloneBrowser.exe file to load the software
4.  Click file>preferences at the top left
5.  For the rclone location: C:\rclone\rclone.exe
6.  For the rclone.conf location: C:\Users\username\AppData\Roaming\rclone\
7.  Check all of the options underneath
8.  gdrive and crypt remotes will now appear in Rclone Browser
9.  Upload all files to crypt remote.
10. If your upload speeds are slow, you may try File>Preferences then add the following line to Default Upload Options: --drive-chunk-size 1024M --transfers=45 --checkers=50 (I'm on a 200/200 connection with 16GB RAM. This took my upload speed from 10MBps to 25MBps. Your mileage may vary.)

### Setting up Rclone Mount

---

1.  Download/install latest WinFsp and select all of the options during installation: [http://www.secfs.net/winfsp/rel/](http://www.secfs.net/winfsp/rel/)
2.  Download the latest NSSM tool: [https://nssm.cc/download](https://nssm.cc/download)
3.  Extract the NSSM folder to c:\rclone and then cut/paste the 64 bit version nssm.exe from the win64 folder into c:\rclone
4.  Open CMD as Admin and navigate to `c:\rclone`
5.  Type nssm install to open the GUI
6.  Applications: Path: `C:\rclone\rclone.exe`
7.  Startup Directory: `C:\rclone`
8.  Arguments:

`mount --dir-cache-time 72h --drive-chunk-size 64M --log-level INFO --vfs-read-chunk-size 32M --vfs-read-chunk-size-limit off crypt: X: --config "C:\Users\username\AppData\Roaming\rclone\rclone.conf" --vfs-cache-mode full`

(Make sure you change the username in path above. You can also choose a different drive letter if desired.)

(Also, these arguments were modified from [u/pierce3215](https://www.reddit.com/u/pierce3215/)'s guide written in 2019 and may or may not be optimal. So far, they have worked for me.)

9. Service Name: `gcrypt`

10. Under Exit Actions tab, choose Restart Application from dropdown, type 10000 in Delay Restart By \_\_ ms field

11. You should now see a folder that says gcrypt (X:) under your Windows Explorer. If not, type: nssm start gcrypt

12. Right-click mounted drive in Explorer (X:) and choose "Properties". Set folder type to "Documents" and apply to all sub folders. This way Explorer will only display attributes that Rclone fetches from the server by default. Otherwise, directories with more than ~5 files will take forever to load and hang/crash Explorer.
13.

#### Setting up Plex

1.  Go to Server Settings
2.  Under Library, disable:

"Empty trash automatically after every scan"

"Generate video preview thumbnails"

"Generate chapter thumbnails"

3. Under Scheduled Tasks, disable:

“Perform extensive media analysis during maintenance”

4. Disabling these options will prevent you from getting API banned by Google.

5. From this point forward, you will setup Plex just as you always do but select the X: folder location that is remotely mounted as your media source.

All done. Now you have an encrypted folder in your Workspace account. If you try to view the contents of your encrypted folder via your Workspace account, all you'll see is encrypted directories/files (and so will Google!). The files will only be viewable from your PC, or any PC that has your Rclone config file. Enjoy!
