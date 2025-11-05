# 4.Execution_of_NetworkCommands
# NAME: SANKAR S
# DEPT: B.E/CSE
# REG NO: 212224040291

## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Program
client.py
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter the website you want to ping (or type 'exit' to quit): ")
    s.send(ip.encode('utf-8'))
    if ip.lower() == 'exit':
        break
    print(s.recv(4096).decode('utf-8'))

s.close()
```
server.py
```
import socket, subprocess, platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server running...")

c, addr = s.accept()
print("Connected:", addr)

while True:
    host = c.recv(1024).decode()
    if not host or host.lower() == 'exit':
        break
    try:
        cmd = ['ping', '-n' if platform.system() == 'Windows' else '-c', '4', host]
        result = subprocess.run(cmd, capture_output=True, text=True)
        c.send(result.stdout.encode())
    except Exception as e:
        c.send(f"Error: {e}".encode())

c.close()


```
## Output

<img width="1427" height="688" alt="image" src="https://github.com/user-attachments/assets/ee5b3822-1c40-4861-b79e-736551fa5fff" />

## Result
Thus Execution of Network commands Performed 
