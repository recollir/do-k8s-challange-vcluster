# do-k8s-challange-vcluster
DigitalOcean Kubernetes Challenge - Deploy a virtual cluster solution

From the [DigitalOcean Kubernetes Challange](https://www.digitalocean.com/community/pages/kubernetes-challenge) homepage:

> Install [vcluster](https://www.vcluster.com/) to test upgrades (eg. 1.20 to 1.21 DOKS version) of your cluster. With a virtual cluster, you can create a new Kubernetes cluster inside your existing DOKS cluster, test the application in this new vcluster, and then upgrade your original cluster if everything works well with the new version. Blogpost: [High-Velocity Engineering with Virtual Kubernetes Clusters](https://loft-sh.medium.com/high-velocity-engineering-with-virtual-kubernetes-clusters-7df929ac6d0a)


## Preparations

- Install doctl
```
brew install doctl
```
- Create API token  
Go to [DO API tokens](https://cloud.digitalocean.com/account/api/tokens\)
- Authenticate doctl
```
doctl auth init
```
- Create Kubernetes cluster
```
doctl kubernetes cluster create k8s-challenge --version 1.21.5-do.0 --count 3 --size s-4vcpu-8gb --region fra1
```
