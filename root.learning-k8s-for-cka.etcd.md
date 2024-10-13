etcdctl is utility that runs commands on

etcdctl snapshot save

etcdctl endpoint health

etcdctl get

etcdctl put

Default port for etcd is 2379. Parameter advertise-client-urls declares the address and port the etcd listens to. This URL should be configured at the Kube API server when it tries to reach etcd server.

kubeadm deploys etcd as a pod in the kube-system namespace.

k8s stores info in a special directory structure. The root dir is registry, under that various k8s constructs - minions, nodes, pods, replica sets, deployments etc.

In a high availability environments there will be multiple master nodes in a cluster, and multiple etcd instances. make sure etcd instances know about each other by setting the parameter in etcd configuration.

Apart from that, you must also specify path to certificate files so that ETCDCTL can authenticate to the ETCD API Server. The certificate files are available in the etcd-master at the following path. We discuss more about certificates in the security section of this course. So don't worry if this looks complex:

--cacert /etc/kubernetes/pki/etcd/ca.crt     
--cert /etc/kubernetes/pki/etcd/server.crt     
--key /etc/kubernetes/pki/etcd/server.key

So for the commands I showed in the previous video to work you must specify the ETCDCTL API version and path to certificate files. Below is the final form:

kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt  --key /etc/kubernetes/pki/etcd/server.key" 
