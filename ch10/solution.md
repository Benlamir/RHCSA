### Lab 10.1

1. Launch the command **dd if=/dev/zero of=/dev/null** three times as a background job.
    ,,,
    dd if=/dev/zero of=/dev/null &
    dd if=/dev/zero of=/dev/null &
    dd if=/dev/zero of=/dev/null &
    ,,,
2. Increase the priority of one of these commands using the **nice** value **5**. Change the priority of the same process again, but this time use the value **15**. Observe the difference.
    ,,,
    renice -n 5 3176
    renice -n 15 3176  
    ,,,
3. Kill all the **dd** processes you just started.
    ,,,
    killall dd
    ,,,
4. Ensure that **tuned** is installed
and active, and set the profile that works best for a virtual machine
that runs on a laptop that is not connected to a power supply.
    ,,,
    systemctl status tuned (if enabled OK)
    systemctl enable --now tuned (if desabled)
    dnf -y install tuned (if not installed)
    tuned-adm active (to see wich profile is activated, balaced profile is set by default)
    tuned-adm list (to see the list of avalable profiles)
    tuned-adm recommend (ti see recommended profile for the machine)
    tuned-adm profile powersave (recommended for saving batterie)
    ,,,
