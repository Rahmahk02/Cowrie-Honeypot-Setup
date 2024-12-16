# Cowrie Honeypot Setup

This repository explains how to set up the Cowrie honeypot. Cowrie logs brute-force attacks and shell interactions from SSH and Telnet, tracking unauthorized access attempts and providing insights into attacker behavior.

## Setup Instructions

The instructions for deploying a Honeypot. Follow the steps below!

## 1. Changing the Default SSH Port

To ensure security, change the default SSH port. For example, it should look similar to this:

```bash
ssh user@1.111.111.1 -p 55555
```
Then, make sure to modify the SSH configuration:
```bash
sudo nano /etc/ssh/sshd_config
```
```bash
sudo systemctl restart ssh
```
## 2. Installing Python Dependencies
```bash
sudo apt update
```
```bash
sudo apt upgrade
```
```bash
sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind virtualenv
```
## 3. Creating/Adding a User for the Honeypot
   
```bash
sudo adduser --disabled-password cowrie
```
```bash
su - cowrie
```

## 4. Clone the Cowrie Repository from the GitHub directory
```bash
git clone https://github.com/cowrie/cowrie
```
```bash
cd cowrie
```
## 5. Set up a Virtual Environment 
```bash
virtualenv cowrie-env
```
```bash
source cowrie-env/bin/activate
```
```bash
pip install --upgrade pip
```
```bash
pip install -r requirements.txt
```
## 6. Configure Cowrie

```bash
cp /etc/cowrie.cfg.dist cowrie.cfg
```

## 7. Set Up a Network Redirection (iptables)

```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222
```
```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport 23 -j REDIRECT --to-port 2223
```
## 8. Start Cowrie's honeypot
```bash
bin/cowrie start
```
## 9. View the Honeypot Logs/Activity
Finally, to view the honeypot logs, use: 
```bash
tail -f ./var/log/cowrie/cowrie.log
```
