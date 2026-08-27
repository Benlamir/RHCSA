### Lab 12.1

1. Create a cron job that performs an update of all software on your computer every evening at 11 p.m.
    ,,,
    0 23 * * * /usr/bin/dnf update -y
    ,,,
2. Schedule your machine to be rebooted at 3 a.m. tomorrow morning.
    ,,,
    at 3:00 tomorrow
    > /sbin/reboot
    > <CTRL+D>
    ,,,
3. Use a Systemd timer to start the vsftpd service five minutes after your system has started.
    ,,,
    1. make sure the vsftpd.service is desabled so thta it does not start on boot
    2. vim /etc/systemd/system/vsftpd.timer
        ,,,
        [Unit]
        Description=Starts the vsftpd 5min after boot

        [Timer]
        OnBootSec=5min
        Unit=vsftpd.service

        [Install]
        WantedBy=timer.target
        ,,,
    systemctl daemon.reload
    systemctl enable --now vsftpd.timer
    systemctl list-timers | grep vsftpd
