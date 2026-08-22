### Lab 11.1

1. Install the vsftpd and httpd services.
    ,,,
    sudo -i
    dnf -y install vsftpd httpd
    ,,,
2. Set the default **systemctl** editor to **vim**.
    ,,,
    export EDITOR=/usr/bin/vim
    ,,,
3. Edit the httpd.service unit file such that
starting httpd will always auto-start vsftpd. Edit the httpd service
such that after failure it will automatically start again in 10 seconds.
    ,,,
    systemctl edit httpd.service
    ,,,
    [Unit]
    Wants=vsftpd.service

    [Service]
    Restart=on-failure
    RestartSec=10s
    ,,,

4. Make sure both services are automatically started while booting.
    ,,,
    systemctl enable --now vsftpd httpd
    ,,,
