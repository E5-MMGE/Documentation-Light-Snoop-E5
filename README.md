# Conf

Switch :
```
en
conf t
vlan 2
name Proxmox
vlan 3
name Wifi
test
int range g0/1-2
switch access vlan 2

int g0/19
switch access vlan 3

int g0/20
switch mode trunk

end
write memory
```

# Doc
