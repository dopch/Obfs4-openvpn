# Obfs4-openvpn
Obfs4-openvpn Obfuscate your openvpn traffic through obfs4.

**obfs4.config on server side can be edited to obfuscate other type of traffic**

### Copyright
https://github.com/gumblex/ptproxy

https://gitlab.com/yawning/obfs4

https://www.torproject.org/

# Installation

To use Obfs4-open you need:
  * An openvpn up and running
  * An openvpn client
  * Python 3.5
  * Build or install obfs4proxy on server and client (https://gitlab.com/yawning/obfs4) 

Here is the file&directory structure :

```
Obfs4-openvpn
├── client
│   ├── bin
│   │   ├── obfs4proxy
│   │   ├── ptproxy.py
│   │   ├── requirements.txt
│   │   └── socksserver.py
│   ├── config
│   │   └── yourconfig.json
│   ├── pkg
│   │   ├── get-pip.py
│   │   └── Runpip
│   └── Run_obfs4proxy
├── LICENSE
├── README.md
└── server
    ├── obfs4.config
    └── obfs4proxy.service
```

### Configuration on server side
You will need to edit obfs4proxt.service and obfs4.config 

obfs4proxy.service line you will need to edit  :

```
EnvironmentFile=/YOURPATH/obfs4.config
ExecStart=/YOURPATH/obfs4proxy -enableLogging true -logLevelStr INFO
```

obfs4.config line you will need to edit  :

```
TOR_PT_STATE_LOCATION=/YOURPATH/obfs4
## Where obfs4proxy will listen IP:port                                                                   
TOR_PT_SERVER_BINDADDR=obfs4-0.0.0.0:80
## Destination for packet receive on TOR_PT_SERVER_BINDADDR, here to openvpn here listening on localhost port 443          
TOR_PT_ORPORT=127.0.0.1:443
```

### Start obfs4proxy on server side 
systemctl start obfs4proxy.service
systemctl enable obfs4proxy.service

To get status and your **CERT (Required by client)**

systemctl status obfs4proxy.service

```
Jun 07 02:51:41 MACHINE1 systemd[1]: Started Obfsproxy Server.
Jun 07 02:51:41 MACHINE1 obfs4proxy[31956]: VERSION 1
Jun 07 02:51:41 MACHINE1 obfs4proxy[31956]: SMETHOD obfs4 [::]:80 ARGS:cert=CERT YOU NEED FOR YOUR CLIENT,iat-mode=0   
Jun 07 02:51:41 MACHINE1 obfs4proxy[31956]: SMETHODS DONE
```
