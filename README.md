## Preparing the FortiGate for Ansible
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

3. Update LAN gateway address
- Change <IP-GATEWAY> and <SUBNET-MASK> accordingly
- Note: Will disconnect your current session and you must reconnect with new IP gateway
```
config system interface
    edit "lan"
        set ip <IP-GATEWAY> <SUBNET-MASK>
    next
end
```

4. Set HTTPS API port
- Note: Will disconnect your current session and you must reconnect with new HTTPS port
```
config system global
    set admin-sport 8665
end
```
