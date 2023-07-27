To mount a NAS folder permanently in Ubuntu, you can add an entry to the `/etc/fstab` file. Here's how you can do it:

1. Open a terminal and run the following command to open the `/etc/fstab` file in a text editor with root privileges:

   ```
   sudo nano /etc/fstab
   ```

2. In the `/etc/fstab` file, add a new line at the end for your NAS mount. The general format is as follows:

   ```
   //<NAS_address>/<shared_folder> /mnt/local/media cifs username=<username>,password=<password>,uid=<your_user_id>,gid=<your_group_id>,rw 0 0
   ```

   Replace `<NAS_address>` with the IP address or hostname of your NAS, `<shared_folder>` with the name of the shared folder you want to mount, `<username>` with your NAS username, `<password>` with your NAS password, `<your_user_id>` with your user ID (you can find it by running the `id -u` command in the terminal), and `<your_group_id>` with your group ID (you can find it by running the `id -g` command in the terminal).

   For example:

   ```
   //192.168.1.100/shared_folder /mnt/local/media cifs username=myusername,password=mypassword,uid=1000,gid=1000,rw 0 0
   ```

   Note: If your NAS supports guest access, you can omit the `username` and `password` options from the line.

3. After adding the line, press `Ctrl+O` to save the changes, and then press `Ctrl+X` to exit the text editor.

4. To test if the `/etc/fstab` entry is correct and mount the NAS folder, run the following command:

   ```
   sudo mount -a
   ```

   This command will attempt to mount all entries in `/etc/fstab`. If there are no errors, the NAS folder should be mounted to `/mnt/local/media`.

5. Reboot your system, and the NAS folder should be automatically mounted to `/mnt/local/media` during startup.

Make sure to replace the placeholders `<NAS_address>`, `<shared_folder>`, `<username>`, `<password>`, `<your_user_id>`, and `<your_group_id>` with your actual NAS details and user information.

Now, whenever you start your Ubuntu system, the NAS folder will be automatically mounted to the specified directory.