---
id: ft5to3veq3u76flq3437zpc
title: Kube Controller Manager
desc: ''
updated: 1719156344868
created: 1719156344868
---
Kube Controller Manager

a controller is like an office or department within the mastership, that have their own set of responsibilities. Is a process that continuosly monitors the state of various components within the system, working towards bringing the whole system to the desired functioning state.

Node-Controller is responcible for monitoring the status of the nodes and taking necessary actions to keep the applications running, does that through the Kube-API server. Node controller tests the status of the nodes every 5 seconds. That way it can monitor the health of the nodes. If it stops receiving the heartbeat from the node, this node is marked unreachable. It waits for 40 sec before marking it so. After marking, it gives it 5 minutes to come back up. If it doesn't, it removes the pods assigned to that node and provisions them on the healthy ones if the PODs are a part of replica set. 

The replication controller. Responsible of monitoring the status of replica sets and ensuring that the desired number of Pods are available at all times within the set. If a Pod dies, it creates another one. 

Those were just two expamples of controllers. 
