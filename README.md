# packVirt
![][image_ref_xgh]
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


[image_ref_xgh]:
data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRw%0D%0AOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjIwIj48bGluZWFy%0D%0AR3JhZGllbnQgaWQ9ImIiIHgyPSIwIiB5Mj0iMTAwJSI+PHN0b3Agb2Zmc2V0PSIwIiBzdG9wLWNv%0D%0AbG9yPSIjYmJiIiBzdG9wLW9wYWNpdHk9Ii4xIi8+PHN0b3Agb2Zmc2V0PSIxIiBzdG9wLW9wYWNp%0D%0AdHk9Ii4xIi8+PC9saW5lYXJHcmFkaWVudD48Y2xpcFBhdGggaWQ9ImEiPjxyZWN0IHdpZHRoPSIx%0D%0AMDAiIGhlaWdodD0iMjAiIHJ4PSIzIiBmaWxsPSIjZmZmIi8+PC9jbGlwUGF0aD48ZyBjbGlwLXBh%0D%0AdGg9InVybCgjYSkiPjxwYXRoIGZpbGw9IiM1NTUiIGQ9Ik0wIDBoMzV2MjBIMHoiLz48cGF0aCBm%0D%0AaWxsPSIjOTdjYTAwIiBkPSJNMzUgMGg2NXYyMEgzNXoiLz48cGF0aCBmaWxsPSJ1cmwoI2IpIiBk%0D%0APSJNMCAwaDEwMHYyMEgweiIvPjwvZz48ZyBmaWxsPSIjZmZmIiB0ZXh0LWFuY2hvcj0ibWlkZGxl%0D%0AIiBmb250LWZhbWlseT0iRGVqYVZ1IFNhbnMsVmVyZGFuYSxHZW5ldmEsc2Fucy1zZXJpZiIgZm9u%0D%0AdC1zaXplPSIxMTAiPiA8dGV4dCB4PSIxODUiIHk9IjE1MCIgZmlsbD0iIzAxMDEwMSIgZmlsbC1v%0D%0AcGFjaXR5PSIuMyIgdHJhbnNmb3JtPSJzY2FsZSguMSkiIHRleHRMZW5ndGg9IjI1MCI+WEdIPC90%0D%0AZXh0Pjx0ZXh0IHg9IjE4NSIgeT0iMTQwIiB0cmFuc2Zvcm09InNjYWxlKC4xKSIgdGV4dExlbmd0%0D%0AaD0iMjUwIj5YR0g8L3RleHQ+PHRleHQgeD0iNjY1IiB5PSIxNTAiIGZpbGw9IiMwMTAxMDEiIGZp%0D%0AbGwtb3BhY2l0eT0iLjMiIHRyYW5zZm9ybT0ic2NhbGUoLjEpIiB0ZXh0TGVuZ3RoPSI1NTAiPkNv%0D%0AbXBpbGFudDwvdGV4dD48dGV4dCB4PSI2NjUiIHk9IjE0MCIgdHJhbnNmb3JtPSJzY2FsZSguMSki%0D%0AIHRleHRMZW5ndGg9IjU1MCI+Q29tcGlsYW50PC90ZXh0PjwvZz4gPC9zdmc+