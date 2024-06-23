---
id: 7qcng3gouzr8pea294ultmy
title: Kube API Server
desc: ''
updated: 1719156353413
created: 1719156353413
---
kube-api server

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

--etcd-servers-https://127.0.0.1:2379 \ specify the location of the etcd servers

how do you view the kube-apiserver options in an existing cluster? depend how you set up your cluster. if you set up with a lubeadmin tool, it deploys the kubeadmin-apiserver as a pod in the kube-system namespace on the master node. options can be seen in the pod definition file at etc/kubernetes/manifest folder.

in a non-kubeadmin setup, you can inspect the options by viewing the kube-apiserver service located at etc/systemd/system/kube-apiserver.service

also, list ps -aux | grep kube-apiserver on the master node
