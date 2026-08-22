### Lab 4.1

1. Describe two ways to show line 5 from the /etc/passwd file.
    ,,,
    method1:
        head -n5 /etc/passwd | tail -n1
    method2:
        sed -n '5p' /etc/passwd
    ,,,
2. How would you locate all text files on your server that contain the current IP address? Do you need a regular expression
    ,,,
    grep -r <"ip adress"> /etc/ 
    you do not need regex if you know the complete ip adress
    ,,,
to do this?
3. You have just used the **sed** command that replaces all occurrences of the text *Administrator* with *root*. Your Windows administrators do not like that very much. How do you revert?
    ,,,
    sed -i 's/root/Administrator/g' <Myfile>
    ,,,
4. Assuming that in the **ps aux**
command the fifth line contains information about memory utilization,
how would you process the output of that command to show the process
that has the heaviest memory utilization first in the results list?
    ,,,
    student@server1:~$ ps aux | sort -nrk4
    ,,,
5. Which command enables you to filter the sixth column of **ps aux** output?
    ,,,
    ps aux | awk '{print $6}'
    ,,,
6. How do you delete the sixth line from the file ~/myfile?
    ,,,
    sed -i '6d' ~/myfile
    ,,,
