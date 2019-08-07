# packVirt
Have you ever wanted a `packstack --allinone` but for oVirt?
I did, so here you go!

---
#### Currently supported versions (and tested)

oVirt Node-ng:
-  [4.3.5-2019080513](https://resources.ovirt.org/pub/ovirt-4.3/iso/ovirt-node-ng-installer/4.3.5-2019080513/el7/)


RedHat Virtualization Host:
- [RHV 4.3 Async#4](https://access.redhat.com/downloads/content/415/ver=4.3/rhel---7/4.3/x86_64/product-software)


I'll get around to making a installation how to, but in lieu of that:

Clone this and get it to the node.

-  RHVH requires your to be registered or have the RHV-M Appliance on hand to install. That being said if you choose the RHVH install route place the appliance in /root/ the ansible will find it and adjust accordingly.


I have been building inside of KVM with: 
- 3 disks
  - 100GB (OS)
  - 60GB (engine)
  - 200GB (vmstore) # optional
- 1+ nics
- 6 vcpu # you could probably go lower but minimum of 2
- 16GB ram # you could probably go lower but minimum of 9GB (unless you adjust the req's for engine)


---
# But whats it do?
- Deploys a self-hosted engine inside of 1 node with gluster mounts

engine.(rhvh|ovirt) will always be +1 of your nodes IP

For example if your node is 192.168.122.100
Your engine will be 192.168.122.101

The domain is based of the install medium, .rhvh or .ovirt 

You will have to add engine.(rhvh|ovirt) to your local machines `/etc/hosts` file in order to access engine

For example:
```
192.168.122.101 engine.rhvh
192.168.122.111 engine.ovirt
```

Engine's username/password: admin/password


---
### How to run
ssh to your node and ```[root@node ~]# ansible-playbook main.yml```