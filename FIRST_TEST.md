# First tests
In Zabbix go to hosts and select Zabbix-server  -> configuration  
At the right-hand of side Groups hit select and tick linux servers and  
templates/databases and then press Update 
## Get stress application 
```shell script
   sudo -s
   yum install -y strees
```
in a console 
type  
```shell script
    uptime 
    sudo stress --cpu  8 --timeout 20  
```


