# ubuntu.nomad-client

Hashicorp nomad setup for Ubuntu.

- https://github.com/Monadical-SAS/ubuntu.nomad-client
- https://github.com/hashicorp/nomad
- https://github.com/jovandeginste/nomad-compose
- https://www.nomadproject.io/docs/configuration/index.html

```fish
git clone https://github.com/Monadical-SAS/ubuntu.nomad-client /opt/ubuntu.nomad-client
cd /opt/ubuntu.nomad-client

# Configure the installation
nano config.env
source config.env
envsubst < etc/nomad/client.llhcl.template > etc/nomad/client.hcl
nano etc/nomad/client.hcl

# Then run the install & start nomad
./bin/setup
systemctl status nomad
nomad status
```
