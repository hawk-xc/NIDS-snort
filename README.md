# NIDS-snort
snort adalah sebuah tools IDS atau difokuskan pada tipe NIDS (Network Intrusion Detection System), snort dapat mendeteksi berbagai intrusi pada jaringan komputer, dan dapat difungsi kan sebagai IPS atau (Intrusion Prevention System)

Pada modul kali ini saya akan mencoba melakukan installasi dan penerapan snort pada Karnel Linux CentOS 7 - RHEL
```
Static hostname: localhost.localdomain                                                                                        
Icon name: computer-vm                                                                                                   
Chassis: vm                                                                                                         
Machine ID: 1178e304bb984e2589d6ccffa0b314dc                                                                               
Boot ID: 186841ab9c914a7ab96b89c2dc1f6de1     
Virtualization: vmware                                                                                                
Operating System: CentOS Linux 7 (Core)                                                                                      
CPE OS Name: cpe:/o:centos:centos:7                                                                                          
Kernel: Linux 3.10.0-1160.el7.x86_64                                                                             
Architecture: x86-64                         
```

### Prerequire
- Internet connection
- Linux CentOS 7 OS

### Installation
```bash
suod su
```

```bash
yum update -y
```

```bash
yum install epel-release bison flex gcc make libdnet libdnet-devel libpcap wget libpcap-devel -y 
 ```
 
 ```bash
 wget https://www.snort.org/downloads/snort/snort-2.9.19-1.centos.x86_64.rpm
 wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz
 ```
 
 ```bash
 tar zxf daq-2.0.7.tar.gz
 ```
 
 ```bash
 cd daq-2.0.7
 ```
 
 ```bash
 ./configure
 ```
 ```bash
 make && make install && cd ..
 ```
 ```bash
 yum install snort-2.9.19-1.centos.x86_64.rpm -y
 ```
 configure
 ```bash
 vi /etc/snort/snort.conf
 ```
 ```
 ipvar HOME_NET 192.168.2.0/24
 # dynamicdetection directory /usr/local/lib/snort_dynamicrules
   whitelist /etc/snort/whitelist/white_list.rules, \                                                                                                                    blacklist /etc/snort/blacklist/black_list.rules
 ```
 ```bash
 mkdir whitelist blacklist
 touch whitelist/white_list.rules blacklist/black_list.rules
 cd /etc/snort/rules
 ```
 ```bash
 touch classification.config reference.config app-detect.rules attack-responses.rules backdoor.rules bad-traffic.rules blacklist.rules blacklist.rules browser-chrome.rules browser-firefox.rules browser-ie.rules browser-other.rules browser-plugins.rules browser-webkit.rules chat.rules content-replace.rules ddos.rules dns.rules dos.rules experimental.rules exploit-kit.rules exploit.rules file-executable.rules file-flash.rules file-identify.rules file-image.rules file-multimedia.rules file-office.rules file-other.rules file-pdf.rules finger.rules ftp.rules icmp-info.rules icmp.rules imap.rules indicator-compromise.rules indicator-obfuscation.rules indicator-shellcode.rules info.rules malware-backdoor.rules malware-cnc.rules malware-other.rules malware-tools.rules misc.rules multimedia.rules mysql.rules netbios.rules nntp.rules oracle.rules os-linux.rules os-other.rules os-solaris.rules os-windows.rules other-ids.rules p2p.rules phishing-spam.rules policy-multimedia.rules policy-other.rules policy.rules policy-social.rules policy-spam.rules pop2.rules pop3.rules protocol-finger.rules protocol-ftp.rules protocol-icmp.rules protocol-imap.rules protocol-pop.rules protocol-services.rules protocol-voip.rules pua-adware.rules pua-other.rules pua-p2p.rules pua-toolbars.rules rpc.rules rservices.rules scada.rules scan.rules server-apache.rules server-iis.rules server-mail.rules server-mssql.rules server-mysql.rules server-oracle.rules server-other.rules server-webapp.rules shellcode.rules smtp.rules snmp.rules specific-threats.rules spyware-put.rules sql.rules telnet.rules tftp.rules virus.rules voip.rules web-activex.rules web-attacks.rules web-cgi.rules web-client.rules web-coldfusion.rules web-frontpage.rules web-iis.rules web-misc.rules web-php.rules x11.rules local.rules botnet-cnc.rules
 ```
 
 ```bash
 ln -s /usr/lib64/libdnet.so.1.0.1 /usr/lib64/libdnet.1
 ```
 
 ### Rules configuration
 
 ```bash
 vi /etc/snort/rules/local.rules
 ```
 add icmp rules
 ```
 alert icmp any any -> any any (msg:"WARNING!!! ICMP PACKET DETECTED"; sid:10001; rev:1001;)
 ```
