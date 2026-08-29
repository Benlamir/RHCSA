### Lab 13.1

1. Configure the journal to be persistent across system reboots.
    ,,,
    sudo -i
    mkdir /var/log/journal
    mkdir /etc/systemd/journald.conf.d
    vim /etc/systemd/journald.conf.d/persistent-logs.conf
        ,,,
        [Journal]
        Storage=persistent
        SystemMaxUse=1G
        ,,,
        :wq
    systemctl restart systemd-journal-flush
    ,,,     SystemMaxUse=1G
    ,,,
    :wq
systemctl restart systemd-journal-flush
,,,
2. Make a configuration file that writes all messages with an info priority to the file /var/log/messages.info.
    ,,,
    vim /etc/rsyslog.d/messages-info.conf
        ,,,
        *.info /var/log/messages.info
        ,,,
        :wq
    systemctl restart rsyslog
    ,,,
3. Configure logrotate to keep 10 old versions of log files.
    ,,,
    vim /etc/logrotate.conf
        ,,,
        rotate 10
        ,,,

