### Lab 9.1

1. List the repositories currently in use on your server.
    ,,,
    dnf repolist
    ,,,
2. Search for the package that contains the cache-only DNS name server. Do not install it yet.
    ,,,
    dnf search "caching DNS"
    ,,,
3. Perform an extensive query of the package so that you know before you install
it which files it contains, which dependencies it has, and where to find the documentation and configuration.
    ,,,
    dnf info dnsmasq.x86_64
    dnf deplist dnsmasq.x86_64
    dnf repoquery -l dnsmasq.x86_64
    ,,,
4. Check whether the RPM package contains any
scripts. You may download it, but you may not install it yet; you want
to know which scripts are in a package before actually installing it,
right?
    ,,,
    rpm -qp --scripts dnsmasq-2.90-4.el10.x86_64.rpm
    ,,,
5. Install the package you found in step 3.
    ,,,
    sudo dnf install -y dnsmasq-2.90-4.el10.x86_64.rpm
    ,,,
6. Undo the installation.
    ,,,
    dnf history
    sudo dnf history undo 12
    ,,,
7. Log in as user student and install the Firefox application in such a way that it is available for that user only.
    ,,,
    flatpak search firefox (result: Firefox)
    flatpak install --user Firefox
    ,,,
