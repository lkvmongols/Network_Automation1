# Network_Automation
@@ -0,0 +1,36 @@
import paramiko
import time

ip_address = "192.168.1.1"
username = "lkv"
password = "mongols"

ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh_client.connect(hostname=ip_address,username=username,password=password)

print "Successful connection", ip_address

remote_connection = ssh_client.invoke_shell()
print "Fetching show ip int br.."

time.sleep(1)
remote_connection.send("show ip int br" + "\n")
output = remote_connection.recv(65535)
print output
time.sleep(2)
remote_connection.send("terminal len 0" + "\n")
output1 = remote_connection.recv(65535)
print output1
time.sleep(2)
print "Fetching show run..."
remote_connection.send("show run" + "\n")
time.sleep(5)
output2 = remote_connection.recv(65535)
print output2
remote_connection.send("exit" +"\n")
time.sleep(1)
output3 = remote_connection.recv(65535)
print output3

ssh_client.close
