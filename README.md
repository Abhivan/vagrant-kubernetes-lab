# vagrant-kubernetes-lab
This project is to provide a simple local Kubernetes cluster with a master and two worker nodes for testing purpose.

Vagrant was chosen for being able to create the cluster either on linux, windows and mac hosts.

## Prequirements
- Vagrant : https://www.vagrantup.com/downloads.html
- VirtualBox : https://www.virtualbox.org/wiki/Downloads

## Default provisioning
Vagrant up will provide 3 Ubuntu Xenial VMs for a kubernetes cluster with these features by default :
- Kubernetes control plane v1.8.6
- Weave network cni v2.0.0
- Kubernetes Dashboard v1.6.1
- Heapster v1.3.0
- Helm v2.7.0

## Kubeconfig
After installation, a copy of the admin.conf generated by kubeadm is available on the host in the vagrant/kubeconfig directory.

Even if kubectl can be used within the guests, it is suggered that you copy the admin.conf as config in your .kube/ directory on the host to able to do kubectl proxy and kubectl port-forward per example.

## Options
It is possible to mount a directory from the host to the /data directory on the k8sworker machine.  This option could be use, for example, to make git repositories local to the host available to be used in the cluster.

The `--mount=<pathOnHost>` option allows to choose the directory on the host that will be mounted to `/data`.  If that option is not specified, `/tmp` on the host will be mounted by default to `/data` on the k8sworker.  For example, run the command:
```
 vagrant --mount=/home/user/git up
```
## Extra features
Multiple optional extra softwares have been tested with this cluster and are available if needed.
Here is the current list by category :
### Ingress
- Nginx ingress controller v0.9.0-beta.15 + Default backend v1.4
### Monitoring
- InfluxDB v1.1.1 + Grafana v4.0.2
- Weavescope v1.5.0
### Networking
- Weave net v2.0.0
- Flannel v0.7.1
### Storage
- Nfs-provisioner v1.0.8
### Helm
- Helm v2.7.0 (tiller)
Installed by default, only helm client is required to fit your host OS : https://github.com/kubernetes/helm/releases
### Jenkins
- Jenkins can be installed on cluster with helm:
  helm --namespace jenkins --name jenkins -f jenkins/jenkins-values.yaml install stable/jenkins
  `jenkins-values.yaml` includes kubernetes plugin and some other essential ones.
##### Have a look at the README.md in related subdirectories for specific instructions.
