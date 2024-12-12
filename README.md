# Ansible Variables
### Generic Settings
```
vdom: root
```

### General Configuration
```
hostname: ansibled-forti
email_to_address: 'someone@somedomain.com'
email_server_reply_to_address: 'someone@somedomain.com'
site_address: '123 Street, Metropolis'
ro_snmp_community_string: Mega
```

### User Configuration
```
admin_username: megaman
admin_password: changeme
```

### Wireless Configuration
```
wifi_controller: false
ssid: fortinet
ssid_password: changeme
```

### DHCP Configuration
```
lan_dhcp_start_address: 192.168.1.100
lan_dhcp_end_address: 192.168.1.250
guest_dhcp_start_address: 192.168.50.100
guest_dhcp_end_address: 192.168.50.250
```

### WAN Configuration
```
pppoe_username: ''
pppoe_password: ''
wan_interface_name: wan
wan_interface_name_pppoe: wan-pppoe
wan_mode: dhcp
wan_vlan: 1
estimated_down_kbps: 25000
estimated_up_kbps: 5000
```

### LAN Configuration
```
lan_interface_name: lan
lan_gateway_address: 192.168.1.99
lan_netmask: 255.255.255.0
```

### GUEST LAN Configuration
```
guest_interface_name: GUEST-VLAN{{ guest_vlan }}
guest_gateway_address: 192.168.50.1
guest_netmask: 255.255.255.0
guest_vlan: 50
```

# Preparing the FortiGate for Ansible
1. Create API user
```
config system api-user
    edit "ansible"
        set accprofile "super_admin"
        set vdom "root"
    next
end
```

2. Generate API key
- Then update vault_admin_key variable with generated API key
```
execute api-user generate-key ansible
```

3. Set HTTPS API port
- Note: Will disconnect your current session and you must reconnect with new HTTPS port
```
config system global
    set admin-sport 8665
end
```

4. Update LAN gateway address
- Change "IP-GATEWAY" and "SUBNET-MASK" accordingly
- Note: Will disconnect your current session and you must reconnect with new IP gateway
```
config system interface
    edit "lan"
        set ip <IP-GATEWAY> <SUBNET-MASK>
    next
end
```
