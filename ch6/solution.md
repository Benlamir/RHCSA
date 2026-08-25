### Lab 6.1

Set up a shared group environment that meets the following requirements:

- Create two groups: sales and account.
    ,,,
    groupadd sales
    groupadd account
    ,,,
- Create users joanna, john, laura, and beatrix.
Make sure they have their primary group set to a private group that has
the name of the user.
    ,,,
    for i in joanna john laura beatrix; do useradd $i; done
    for i in joanna john laura beatrix; do id $i; done
    ,,,
- Make joanna and john members of the group sales and make laura and beatrix members of the group account.
    ,,,
    usermod -aG sales joanna
    usermod -aG sales john
    usermod -aG account laura
    usermod -aG account beatrix
    ,,,
- Set a password policy that requires users to change their password every 90 days.
    ,,,
    for i in joanna john laura beatrix; do passwd -x 90 $i; done
    ,,,

### Lab 6.2

Create a **sudo** configuration that 
allows user bill to manage user properties and passwords but that does 
not allow this user to change the password for the root user.
    ,,,
    sudo sh -c 'echo "bill ALL=/usr/bin/passwd, /usr/bin/usermod, /usr/bin/useradd, ! /usr/bin/passwd root" > /etc/sudoers.d/bill'
    ,,,
    ,,,
    sudo visudo -c ( check the syntaxe should give a parsed ok with chmod 0440 for the sudoers)
