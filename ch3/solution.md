### Lab 3.1

1. Log in as user **student** and use **sudo -i** to open a root shell. In the home directory of root, create one archive file that contains the contents of the /home directory and the /etc
directory. Use the name /root/essentials.tar for the archive file.
,,,
sudo -i
tar -cf /root/essentials.tar /home /etc
,,,
2. Copy this archive to the /tmp directory. Also create a hard link to this file in the /directory.
,,,
cp /root/essentials.tar /tmp && ln /root/essentials.tar /
,,,
3. Rename the file /essentials.tar to **/archive.tar**.
,,,
mv /essentials.tar /archive.tar
,,,
4. Create a symbolic link in the home directory of the user root that refers to /archive.tar. Use the name **link.tar** for the symbolic link.
,,,
cd /root/
ln -s /archive.tar link.tar
,,,
5. Remove the file /archive.tar and see what happens to the symbolic link. Remove the symbolic link also.
,,,
rm -f /archive.tar
rm -f /root/link.tar
,,,
6. Compress the /root/essentials.tar file.
,,,
gzip /root/essentials.tar
,,,
