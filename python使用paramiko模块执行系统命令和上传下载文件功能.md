## 一、目的

使用python的paramiko模块，实现操作系统级别命令和上传下载文件功能



安装模块

```bash
$ pip install paramiko
```





## 二、示例1

```pyt
import paramiko
import sys
import os
def sshExeCMD():
    ssh_client=paramiko.SSHClient()
    ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    ssh_client.connect(hostname="10.10.2.200",port=22,username="root",password="root")

    stdin, stdout, stderr = ssh_client.exec_command("hostname")
    print(stdout.read())
    ssh_client.close()

def sshDf(ip,username,password,port=22):
    ssh_client=paramiko.SSHClient()
    ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    try:
        ssh_client.connect(hostname=ip,port=port,username=username,password=password)
    except Exception as e:
        print("服务器%s连接失败!!!" % ip)
        print(e)
        sys.exit()
    stdin,stdout,stderr=ssh_client.exec_command("df -hT")
    print(stdout.read().decode("utf-8"))
    ssh_client.close()


def sshFile():
    ssh_conn=paramiko.Transport(("10.10.2.200",22))
    ssh_conn.connect(username="root",password="root")
    ftp_client=paramiko.SFTPClient.from_transport(ssh_conn)
    ftp_client.get("/etc/fstab",r"D:\tmp\fstab")
    ftp_client.put(r"D:\tmp\stop.sh","/tmp/stop.sh")
    ssh_conn.close()





if __name__ == '__main__':
    sshExeCMD()

    servers = {
        "10.10.2.200":{
            "username": "root",
            "password": "root",
            "port": 22
        },
        "10.10.2.201":{
            "username": "root",
            "password": "root",
            "port": 22
        }       
    }

for ip,info in servers.items():
    sshDf(
        ip=ip,
        username=info.get("username"),
        password=info.get("password"),
        port=info.get("port")
    )
  
    sshFile()


```







## 三、示例2

```py
import paramiko
import sys
import os


def sshPutFile(ip,port,username,password,localfile,remotedir):
    file_name=os.path.basename(localfile)
    if not remotedir.endswith("/"):
        remotedir=remotedir + "/"
    
    dest_file_name = remotedir + file_name
    ssh_conn=paramiko.Transport((ip,port))
    ssh_conn.connect(username=username, password=password)
    
    ftp_client=paramiko.SFTPClient.from_transport(ssh_conn)
    ftp_client.put(localfile,dest_file_name)
    ssh_conn.close()

if __name__ == '__main__':
    servers = {
        "10.10.2.200":{
            "username": "root",
            "password": "root",
            "port": 22
        }     
    }


source_file=input("请输入源文件绝对路径：")
remote_dir=input("目标目录路径")


for ip,info in servers.items():
        sshPutFile(
        ip=ip,
        username=info.get("username"),
        password=info.get("password"),
        port=info.get("port"),
        localfile=source_file,
        remotedir=remote_dir
    )
```

