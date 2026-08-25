### Lab 7.1

1. Set up a shared group environment. If you haven’t
created these directories in a previous exercise yet, create two
directories: /data/account and /data/sales. Make the group sales the
owner of the directory sales, and make the group account the owner of
the directory account.
    ,,,
    sudo -i
    mkdir -p /datat/account
    mkdir -p /datat/sales
    chown :sales /data/sales
    chown :account /data/account
    ,,,
2. Configure the permissions so that the user owner
(which must be root) and group owner have full access to the directory.
There should be no permissions assigned to the others entity.
    ,,,
    chmod 770 /data/sales
    chmod 770 /data/account
    ,,,
3. Ensure that all new files in both directories
inherit the group owner of their respective directory. This means that
all files that will be created in /data/sales will be owned by the group sales, and all files in /data/account will be owned by the group
account.
    ,,,
    chmod g+s /data/sales
    chmod g+s /data/account
    ,,,
4. Ensure that users are only allowed to remove files of which they are the owner.
    ,,,
    chmod +t /data/sales
    chmod +t /data/account
    ,,,
