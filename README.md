# zervice.nomad-client
Hashicorp nomad setup for Ubuntu.


```fish
function setup_nomad
    echo -e $yellow"\n[+] Setting up Hashicorp Nomad...\n"$normal
    apt_install wget unzip
    
    mkdir -p /opt/zervice.nomad-client/data/nomad
    mkdir -p /opt/zervice.nomad-client/data/tmp
    mkdir -p /opt/zervice.nomad-client/data/logs
    mkdir -p /opt/zervice.nomad-client/etc
    mkdir -p /opt/zervice.nomad-client/bin

    cd /opt/zervice.nomad-client

    wget --continue \
        "https://releases.hashicorp.com/nomad/0.9.5/nomad_0.9.5_linux_amd64.zip" \
        -O ./data/tmp/nomad_linunx_amd64.zip


    unzip data/tmp/nomad_0.9.5_linux_amd64.zip -d bin/
    rm data/tmp/nomad_0.9.5_linux_amd64.zip

    ln -f -s (pwd)/bin/nomad /usr/local/bin/nomad

    nomad -autocomplete-install

    wget --continue \
        "https://raw.githubusercontent.com/hashicorp/nomad/master/dist/systemd/nomad.service" \
        -O (pwd)/etc/nomad.service

    ln -f -s (pwd)/etc/nomad.service /etc/systemd/system/nomad.service
    ln -f -s (pwd)/etc/nomad.hcl /etc/nomad.d/nomad.hcl

    systemctl enable nomad
    systemctl start nomad

    echo -e $green"\n[√] Nomad is set up and is running."$normal
    nomad version
    env SYSTEMD_COLORS=1 systemctl status --no-pager nomad | head -3
end
```
