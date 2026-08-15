1. Modify your shell environment so that on every subshell that is started, a variable is set. The name of the variable should be **COLOR**, and the value should be set to **red**. Verify that it is working.
,,,
vim .bashrc
export COLOR=red
:wq
source .bashrc
,,,

2. Use the appropriate tools to find the command that you can use to change a user password. Do you need root permissions to use this command?
,,,
sudo mandb
man -k user | grep password
passwd
no, if i want to change my passwd. yes, if i want to change the passwd of another user
,,,

3. From your home directory, type the command **ls -al wergihl \**and ensure that errors as well as regular output are redirected to a file with the name /tmp/lsoutput.
,,,
ls -al wergihl * &> /tmp/lsoutput
,,,
