# Deploy a Kubernetes cluster using Vagrant and ansible wiht VirtualBox as provider

> [!NOTE]
> This docs consider that you already have Virtualbox installed.
> And you have Debian/Ubuntu OS based.

## Install Vagrant
You can directly try:
```
apt install vagrant
```

If it presents some errors like `Unable to find package`, try [this docs](https://developer.hashicorp.com/vagrant/downloads)

```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant
```

## Install Ansible
Use the following command:
```
pip3 install ansible ansible-core
```

## Post deployment
Once your cluster deployed, you should have a Kubernetes configuration file in project root directory named `config`.
Install **kubectl** on your OS and copy `config` file to `$HOME/.kube` (/home/_username_/.kube).
If everything is OK, try to get the cluster's nodes using:
```
kubectl get nodes
```
It should print some nodes named **srv-k8s-master** and **srv-k8s-workX**

Try to deploy the simple Nginx server in your cluster:
```
kubectl apply -f deploy-nginx.yml
```