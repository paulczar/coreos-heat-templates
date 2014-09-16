CoreOS Heat Examples
===============

Basic CoreOS Cluster - on VMs
--------------------------------------------

```console
$ heat stack-create CoreOS --template-file=coreos.yml \
 -P name=CoreOS -P etcd_discovery=$(curl -s https://discovery.etcd.io/new)
```

OnMetal
-------------

```console
$ heat stack-create CoreOS --template-file=coreos_metal.yml \
 -P count=1 -P etcd_discovery=$(curl -s https://discovery.etcd.io/new)
```

Log into CoreOS
------------------------
```console
$ eval `ssh-agent`
$ echo $(heat output-show CoreOS private_key | sed 's/"//g') | ssh-add -
$ export LB=$(heat output-show CoreOS loadbalancer | sed 's/"//g') && echo $LB
```