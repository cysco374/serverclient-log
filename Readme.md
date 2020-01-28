# SSH Access Log Attempts


SSH Access log attempts using python. The deployment/configuration is automated with Ansible.
The reporting too has three parts
  - Server.py
  - Client.py
  - Reporter.py

## Setup

The set up is 
- The repo has an Ansible inventory file which is located in **ansible/hosts** add the client and server IP/hostname there.
- Update Reporter.py and Cleint.py with server's IP/hostname
 The server store data in a mysql. The Reporter.py access the data directly from mysql therefore line number 10  need to be updated.
```python 
db_host = 'ip-address-of-server'
```
The client require ip/hostname of server to send data to. Therefore you need to update line 8 on Client.py
```python
server = "ip-address-of-server"
```

The client sends data directly to server's port ***8888***. This port should not be used by any other process. 

The logs go to:
```bash
Client.py >> /var/log/ListenClient.log
Server.py >> /var/log/ListenServer.log 
```
There is a lockfile in /tmp/mydaemon.pid for Client.py. If you are killing process forcefully make sure you remove this file. 

# How to get report
login to the client server and enter command
```bash
Reporter.py
```