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
```
execute api-user generate-key ansible
```

3. Set HTTPS API port
```
config system global
    set admin-sport 8665
end
```
