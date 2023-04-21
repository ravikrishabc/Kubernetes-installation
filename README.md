# Kubernetes-installation
# Kubernetes installation guide on aws in ubuntu

Create an AWS EC2 instance with Ubuntu OS.
Update the instance and install necessary packages by running the following commands:




Note: The --pod-network-cidr option is used to specify the pod network range.




## Update the packages



```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

```

Add the Kubernetes repository by running the following command

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

```

Add the Kubernetes repository by running the following command:
```bash
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"

```
Update the instance again and install Kubernetes packages by running the following commands:
```bash
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl

```

Initialize the Kubernetes cluster by running the following command:

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

```

Note: The --pod-network-cidr option is used to specify the pod network range.

After the initialization is complete, run the following command to set up the kubectl configuration

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config


```
Install the Calico network plugin by running the following command:

```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

```

Wait for a few minutes for the Calico pods to start up and check the cluster status by running the following command:

```bash
kubectl get pods --all-namespaces

```

If everything is working fine, you should see a list of running pods in the output.

Congratulations, you have now installed Kubernetes on AWS running Ubuntu!











