1. Create new ec2 instance
    - AMI: ubuntu 18.04
    - VPC: default
    - Subnet: eu-west-1
    - IP: Enable
    - security group: allow port 3000 and 22, sre_amy_grafana.pem is key
2. Ssh in
3. Run the following as grafana_provision.sh
```bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install -y adduser libfontconfig1
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_8.1.5_amd64.deb
sudo dpkg -i grafana-enterprise_8.1.5_amd64.deb
```

3. Run `sudo nano /etc/apt/sources.list`, then enter the following lines, then save and close:
```
# adding new resources for grafana package from package cloud
deb https://packagecloud.io/grafana/stable/debian/ stretch main
```
5. Run `curl https://packagecloud.io/gpg.key | sudo apt-key add -`
6. `sudo wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_5.2.4_amd64.deb`
7. `sudo apt-get install grafana`
8. run:
```bash
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
sudo systemctl enable grafana-server.service
sudo service grafana-server start
systemctl status grafana-server.service
```
9. `sudo update-rc.d grafana-server defaults`
10. `sudo systemctl enable grafana-server.service`
11. `sudo nano /usr/share/grafana/.credentials`
enter:
```
[default]
aws_access_key_id = <key>
aws_secret_access_key = <key>
region = eu-west-1
```
12. `sudo chmod 0644 /usr/share/grafana/.credentials`
