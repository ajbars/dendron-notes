---
id: 82fsl77vbgtg431vm82d1hc
title: Learning Kubernetes for Cka
desc: ''
updated: 1717614160162
created: 1717613529080
---
**Plan of learning:** 

**Courses:**

Mumshad Mannambeth's course on Udemy

https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/?couponCode=ST19MT60324

**Labs:**

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

etcdctl is utility that runs commands on 

etcdctl snapshot save 

etcdctl endpoint health

etcdctl get

etcdctl put


Default port for etcd is 2379. Parameter advertise-client-urls declares the address and port the etcd listens to. This URL should be configured at the Kube API server when it tries to reach etcd server.

kubeadm deploys etcd as a pod in the kube-system namespace. 

k8s stores info in a special directory structure. The root dir is registry, under that various k8s constructs - minions, nodes, pods, replica sets, deployments etc.

In a high availability environments there will be multiple master nodes in a cluster, and multiple etcd instances. make sure etcd instances know about each other by settimg the parameter in etcd configuration. 

Apart from that, you must also specify path to certificate files so that ETCDCTL can authenticate to the ETCD API Server. The certificate files are available in the etcd-master at the following path. We discuss more about certificates in the security section of this course. So don't worry if this looks complex:

    --cacert /etc/kubernetes/pki/etcd/ca.crt     
    --cert /etc/kubernetes/pki/etcd/server.crt     
    --key /etc/kubernetes/pki/etcd/server.key

So for the commands I showed in the previous video to work you must specify the ETCDCTL API version and path to certificate files. Below is the final form:


    kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt  --key /etc/kubernetes/pki/etcd/server.key" 


**kube-api server**

is the main controlling element 

kubectl is utility that reaches the apiserver. it receives the request, authenticates and validates it. then it retreives the data from etcd cluster

API can be invoked directly by POST request

curl -X POST /api/v1/namespaces/default/pods ...[ other ]

the API server creates a pod object without assigning it to the node, updates the info in the etcd server, updates the user that the pod has been created

the scheduler contiounusly monitors the API server and realizes that there is a new pod with no node assigned

the scheduler identifies the right node to place the new pod on and communicates that back to the API server

the API server then updates the info in the etcd cluster. the API server passes that info to the kubelet in the appropriate worker node

the kubelet then creates the pod on the node and instructs the container runtime engine to deploy the application image

once done, the kubelet updates the status back to the API server and the API server then updates the data back in the etcd cluster

A similar pattern is followed every time a change is requested

The kubeAPI server is at the center of all the different tasks that need to be performed to make a change in the cluster


Summary:

API server is responsible for:

Authentication and validation of the request

Retrieving data

Updating ETCD (as the only component that interacts with it directly)

Scheduler 

Kubelet


Available as a binary in the Kubernetes release page. download and configure it to run as a service on yout k8s master node.

the kubeapi server is run with a lot of parameters

options:

--etcd-servers-https://127.0.0.1:2379 \\ specify the location of the etcd servers 

how do you view the kube-apiserver options in an existing cluster? depend how you set up your cluster. if you set up with a lubeadmin tool, it deploys the kubeadmin-apiserver as a pod in the kube-system namespace on the master node. options can be seen in the pod definition file at etc/kubernetes/manifest folder. 

in a non-kubeadmin setup, you can inspect the options by viewing the kube-apiserver service located at etc/systemd/system/kube-apiserver.service 

also, list ps -aux | grep kube-apiserver on the master node


Kube Controller Manager

a controller is like an office or department within the mastership, that have their own set  




