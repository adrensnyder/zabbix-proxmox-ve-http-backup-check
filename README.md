# Proxmox VE by HTTP – Backup check (Zabbix add-on)
Zabbix Template that enable monitoring of backup status for every hosts that have a desidered tag on Proxmox PVE nodes  

It used to be added to the official [Proxmox VE by HTTP](https://www.zabbix.com/integrations/proxmox) template because it shares many MACROS  
Tested with Proxmox VE by HTTP on Zabbix Server 6.0 LTS

All the MACROS used are explained in the template  

## Instructions
Add an SNMP interface with the IP address of the Proxmox VE node.  
The interface is required by Zabbix to attach the template, but it is not used for data collection.  

Edit macro {$PVE.HOSTNAME} with the hostname of the node  

Create group "zabbix" in Permissions - Groups  
Create user "zabbix" with group "Zabbix" in Permissions - Users  

Create an API token for user "zabbix@xxx" with token id "zabbix"  
Please copy the TokenID and Secret separately as they will not be displayed afterwards  

Create a new role in Roles, or edit it if already exist, named "Zabbix" with:  
Datastore.Allocate  
Datastore.AllocateSpace  
Datastore.Audit  
Pool.Audit  
SDN.Audit  
Sys.Audit  
VM.Audit  

Add/Replace User/Group/Api permission in Permissions with:  
Path: /  
User: [The zabbix User/Group/Api]  
Role: Zabbix  

Note: All the 3 permissions are needed to get the template working  

In the Zabbix Host modify the Macro {$PVE.TOKEN.ID} and {$PVE.TOKEN.SECRET} with the values we saved before  

There credentials are shared across all the nodes  

## Requirements
- Zabbix: 6.0+ (tested on 6.0 LTS)
- Proxmox VE API access via user + API token
