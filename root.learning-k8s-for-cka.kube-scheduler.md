responsible for scheduling pods on nodes. It decides only which pod goes on which node. It doesn't actually place the pod on the nodes. that's the job of the kubelet. the kubelet as the captain of the ship is who creates the pod on the ships. The scheduler only decides which pod goes where.

why do you need a scheduler? when there's many 'ships' and many containers, you want to make sure the right container ends up on the right ship. for example, there could be different sizes of ships and containers. you wanna make sure the ship has sufficient capacity. also different ships may be going to different destinations. 

The scheduler (further will be called S) decides which pods are placed on which nodes depending on certain criteria. Pods may have different resource requirements. Nodes can be dedicated to certain applications. How does S assigns these pods? 

It looks at each pod and tries to find the best node for it. If the pod has the CPU and memory requirements it goes through two-phase process. In the first phase it tries to filter out the nodes that don't fit the profile for this pod. For ex, the nodes that don't have sufficient CPU and memory requested by the pod. Then it ranks the nodes to identify the best fit for the pod. It uses the priority function to assign the score to the nodes on a scale of zero to 10. For example it calculates the amount of resources that would be free on the nodes after placing the pod on them. The one that has more left, win

This can be customized and you can write your own scheduler as well.

How to install the kube scheduler?

Download the binary

wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-scheduler

extract and run as a service

ExecStart=/usr/local/bin/kube-scheduler \\
--config=/etc/kubernetes/config/kube-scheduler.yaml \\
--v=2

How to view the S options

kubeadm:

cat /etc/kubernetes/manifests/kube-scheduler.yaml

see running process and effective options:

ps -aux | grep kube-scheduler


