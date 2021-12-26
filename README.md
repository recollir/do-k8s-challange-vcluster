# do-k8s-challange-vcluster
DigitalOcean Kubernetes Challenge - Deploy a virtual cluster solution

From the [DigitalOcean Kubernetes Challenge](https://www.digitalocean.com/community/pages/kubernetes-challenge) homepage:

> Install [vcluster](https://www.vcluster.com/) to test upgrades (eg. 1.20 to 1.21 DOKS version) of your cluster. With a virtual cluster, you can create a new Kubernetes cluster inside your existing DOKS cluster, test the application in this new vcluster, and then upgrade your original cluster if everything works well with the new version. Blogpost: [High-Velocity Engineering with Virtual Kubernetes Clusters](https://loft-sh.medium.com/high-velocity-engineering-with-virtual-kubernetes-clusters-7df929ac6d0a)


## Preparations - Create a Kubernetes cluster using [DOKS (DigitalOcean managed Kubernetes Service)](https://www.digitalocean.com/products/kubernetes/)

- Install doctl and kubectl
```
brew install doctl
brew install kubectl
```
- Create an API token (to be used in the next step)  
Go to [DO API tokens](https://cloud.digitalocean.com/account/api/tokens)
- Authenticate doctl
```
doctl auth init
```
- Create Kubernetes cluster
```
CLUSTER_NAME=k8s-challenge
doctl kubernetes cluster create $CLUSTER_NAME --version 1.21.5-do.0 --count 3 --size s-4vcpu-8gb --region fra1
```
- Get the Kubernetes cluster name and kubeconf
```
doctl kubernetes cluster list
doctl kubernetes cluster kubeconfig show $CLUSTER_NAME
doctl kubernetes cluster kubeconfig save $CLUSTER_NAME
```
- Check access to the Kubernetes cluster
```
kubectl get nodes
```
- Delete the Kubernetes cluster and kubeconf
```
doctl kubernetes cluster list
doctl kubernetes cluster kubeconfig rm $CLUSTER_NAME
doctl kubernetes cluster rm $CLUSTER_NAME
```

## Install [vcluster](https://www.vcluster.com)

Based on the [_getting started_ full guide](https://www.vcluster.com/docs/getting-started/setup).  
**Requirement:** access to running Kubernetes cluster
- Install the vcluster cli
