import os
from socket import *
from threading import *
from colorama import Fore
screenLock = Semaphore(value=1)
def connScan(tgtHost,tgtPort):
    try:
        conn=socket(AF_INET,SOCK_STREAM)
        conn.connect((tgtHost,tgtPort))
        conn.send('hello world\r\n'.encode("utf-8"))             #发送测试信息给端口
        results=conn.recv(100)                    #接收主机返回的信息
        screenLock.acquire()                      #加锁
        print(Fore.GREEN+'[OPEN]{0}/tcp '.format(tgtPort)+Fore.WHITE+results.decode("utf-8"))
        conn.close()
    except Exception:
        screenLock.acquire()
        #print(e)
        #print(Fore.WHITE+'[CLOSE]%d/tcp'% tgtPort)
    finally:
        screenLock.release()           #释放锁
        conn.close()
def portScan(tgtHost,tgtPorts):
    print(Fore.BLUE+"[LOAD]正在解析IP",end=" ")
    try:
        tgtIP=gethostbyname(tgtHost)          ##获得对应主机的ip地址
        print(Fore.WHITE+'')
    except Exception as e:
        print(Fore.RED+"[ERROR]不能解析%s的IP {0}".format(e) %tgtHost)
        
    try:
        Name=gethostbyaddr(tgtIP)     ##获得ip对应主机的信息
        print (Fore.YELLOW+"\n[INFO]主机信息:"+Name[0])
    except:
        print (Fore.YELLOW+"\n[INFO]主机IP"+tgtIP)

    setdefaulttimeout(1)
    for Port in tgtPorts:
        t = Thread(target=connScan,args=(tgtHost,int(Port)))
        t.start()
    return
    
def main(Host,Ports):
    portScan(Host,Ports)
if __name__=='__main__':
    if os.name == 'nt':
        os.system("cls")
    else:
        os.system("clear")
    print(Fore.LIGHTCYAN_EX+"_______________|_____________>..]>"
                            "\n|liuyyds私藏端口扫描器v1.0(Beta)||>>> - · · >"
                            "\n|Author:liusuxy|___________/-->.>->"
                            "\n|##|->|   ||  |_||| || || ||")
    tgt_host = str(input(Fore.LIGHTMAGENTA_EX+"|URL of target|->"))
    #ip_list = str(input(Fore.LIGHTMAGENTA_EX+"|Port(s) of list|->")).split(",")
    #################################################
    ip_list = [80,443,22,21,4444] #这里设置端口扫描列表
    #################################################
    main(tgt_host,ip_list)
    
