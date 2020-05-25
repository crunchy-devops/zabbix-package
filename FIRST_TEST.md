# First tests
In Zabbix go to hosts and select Zabbix-server  -> configuration  
At the right-hand of side Groups hit select and tick linux servers and then press Update
 
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
    uptime
    sudo stress --cpu 4 --io 3 --vm 2 --vm-bytes 256M --timeout 20s
    uptime
```
## Check the results in zabbix 
Go to graphs and select cpu utilization 

## Set a monitoring screen  
go to screen, and click edit screen       
select the blue text change in down/left this screen     
select resource as graph  
in Graph select zabbix server: CPU utilization  
Horizontal Left , vertical align Top  
and click update  