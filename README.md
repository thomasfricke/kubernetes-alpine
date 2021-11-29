# Installation of Kubernetes on a Alpine Host

## Base

This installation assumes an empty fresh Alpine 3.15

## Configuration

All configurations files are in the `etc` directory. Please review with care and adapt it to your needs.
Especially `fstab` needs to be adapted to your local file system, including uuids.

```bash

etc
├── apk
│   └── repositories
├── cni
│   └── net.d
│       └── 10-crio-ipv4-bridge.conf
├── crictl.yaml
├── fstab
├── install
├── kubeinstall
├── modules-load.d
│   └── k8s.conf
├── ssh
│   └── sshd_config
├── subgid
├── subuid
├── sysctl.conf
└── sysctl.d
    └── k8s.conf

```

The configuration needs to be tared `tar cfz etc.tgz etc` and moved to the Alpine host system.

Untar it in /, the existing configuration will be overwritten

```bash

cd /

tar xfz etc.tgz

```

## Installation

Execute the installation `source /etc/install` and if 
everything works `source /etc/kubeinstall` will create a 
single node cluster. Set the environment variable `KUBECONFIG`

```bash

export KUBECONFIG=/etc/kubernetes/admin.conf


```

For tests with a single node cluster, node taint 
master must be removed from the role.

```bash

kubectl taint nodes --all node-role.kubernetes.io/master-


```

## Cluster

If everything works, you can add further node the usual `kubeadm` way.
