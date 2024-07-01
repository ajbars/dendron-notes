---
id: ft5to3veq3u76flq3437zpc
title: Kube Controller Manager
desc: ''
updated: 1719156344868
created: 1719156344868
---
Kube Controller Manager

a controller is like an office or department within the mastership, that have their own set of responsibilities. Is a process that continuosly monitors the state of various components within the system, working towards bringing the whole system to the desired functioning state.

Node-Controller is responsible for monitoring the status of the nodes and taking necessary actions to keep the applications running, does that through the Kube-API server. Node controller tests the status of the nodes every 5 seconds. That way it can monitor the health of the nodes. If it stops receiving the heartbeat from the node, this node is marked unreachable. It waits for 40 sec before marking it so. After marking, it gives it 5 minutes to come back up. If it doesn't, it removes the pods assigned to that node and provisions them on the healthy ones if the PODs are a part of replica set. 

The replication controller. Responsible of monitoring the status of replica sets and ensuring that the desired number of Pods are available at all times within the set. If a Pod dies, it creates another one. 

Those were just two expamples of controllers. There are many more others available in k8s. All consepts - deployment, services, namespaces, persistent volumes, whatever intelligence is built into these constructs, it is implemented through these various controllers. Kinda brain behind the things in k8s. 

How do you see them and where are they located in your cluster? They are all packaged into a single process known as the K8s Controller Manager. When you install it, different other controllers are installed as well. 

Download kube controller manager from the k8s release page 

wget https://storage.googleapis.com/kubernetes-release/...

Extract and run as a servive

When you run it, there are a list of options provided. This is where you provide additional options to customize your controller. You can specify which controllers to enable.






