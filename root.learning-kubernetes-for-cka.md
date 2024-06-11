---
id: 82fsl77vbgtg431vm82d1hc
title: Learning Kubernetes for Cka
desc: ''
updated: 1717614160162
created: 1717613529080
---
Plan of learning: 

**Courses:
**

Mumshad Mannambeth's course on Udemy

https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/?couponCode=ST19MT60324

**Labs: 
**

https://killercoda.com/cka

**Tips:** 

http://training.linuxfoundation.org/go//Important-Tips-CKA-CKAD
20KODE - 20% discount

**Repo with various stuff:**

https://github.com/kodekloudhub/certified-kubernetes-administrator-course

Open Container Initiative allows to use other container vendors with k8s. It contains imagespec and runtimespec, sets of requirements for images and runtimes.

Now supported containerd and rkt

ctr - tool for containerd, another more recommended is nerdctl tool, docker-like cli


other utility - crictl - provides a CLI for CRI compatible container runtimes. Used to inspect and debug container runtimes. Not to create containers ideally. Works across different runtimes.
Works along with the kubelet.

etcdctl is utility that runs commands on etcd.

Default port for etcd is 2379. Parameter advertise-client-urls declares the address and port the etcd listens to. This URL should be configured at the Kube API server when it tries to reach etcd server.

kubeadm deploys etcd as a pod in the kube-system namespace. 

k8s stores info in a special directory structure. The root dir is registry, under that various k8s constructs - minions, nodes, pods, replica sets, deployments etc.

In a high availability environments there will be multiple master nodes in a cluster, and multiple etcd instances. make sure etcd instances know about each other by settimg the parameter in etcd configuration. 