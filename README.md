# Grafana  
Grafana is an open source analytics & monitoring tool which can be used to monitor your application infrastructure and analyse logs. It is independent, so it can be used with multiple cloud providers, such as AWS or Azure.  

## Setting up Grafana Server
1. Create new ec2 instance  
    - AMI: ubuntu 18.04
    - VPC: default
    - Subnet: eu-west-1
    - IP: Enable
    - Security group: allow port 3000 and 22, sre_amy_grafana.pem is key
    - Tags: `Name`, `SRE_Amy_Grafana`  
2. Ssh into the instance  
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
6. Then run `sudo wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_5.2.4_amd64.deb`  
7. Then run `sudo apt-get install grafana`  
8. Run the following:  
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
12: Run the following commands:
```
[default]
aws_access_key_id = <key>
aws_secret_access_key = <key>
region = eu-west-1
```
13. `sudo chmod 0644 /usr/share/grafana/.credentials`
