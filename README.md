## Open Source Day 2017 Warsaw Ansible+Docker+Azure Workshops

Event will be held at 2017-05-17 15:00 CEST.

Discover how Ansible and Docker enables the process of container
life cycle. Deploy and manage your infrastructure and applications
from single management workstation. Participants will learn how
to effectively use Ansible playbooks for reliable automation and
compliance.

Just bring your own laptop with **ssh client** and **web browser**
installed - this interactive workshop will employ **Ansible** to deploy
**Docker** cluster on **Azure** cloud to bootstrap test invironments in
just few minutes!

### Materials

Slides are available [here](https://bit.ly/adaslides).

Demo (in Polish):

[![asciicast](https://asciinema.org/a/a14fkwwz9hfrych4z0sp045la.png)](https://asciinema.org/a/a14fkwwz9hfrych4z0sp045la)

Hint: you can copy-and-paste from this Asciicast :)

[![youtube](http://img.youtube.com/vi/hzjcpoNOL8w/0.jpg)](http://www.youtube.com/watch?v=hzjcpoNOL8w)

### Lab Replay

Replay this lab at home by following easy steps:

1. Register free account on Docker Hub: https://hub.docker.com/
1. Install Azure CLI: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli
1. Download this repository (green button in top right corner of github page)
1. Edit ```azuredeploy.parameters.json``` and insert your ```servicePrincipalClientId``` and ```servicePrincipalClientSecret``` (```sshRSAPublicKey``` will be auto-generated)
1. Install Azure kubernetes cluster with provided ```deploy``` script
1. Check your cluster IP address with ```az acs list'''
1. Login onto "developement" VM: ```ssh -i .ssh/az_acs azureuser@...```
   1. We will use example Wordpress (app+database) docker set: ```cd examples/wordpress```
   1. Examine set of containers (```container.yml```) and provided ansible playbook (```main.yml```)
   1. First we build our images: ```ansible-container build```
   1. Now we can run them (interactively, or with ```-d``` option - in backgroud): ```ansible-container run [-d]```
   1. (Point your browser to http://YOUR-ACS-INSTANCE and play with Wordpress demo)
   1. Login from your developement to Docker Hub: ```docker login```
   1. Push your applications to Docker Hub: ```ansible-container push```
   1. Examine pushed images (check "Tags" tab) on Docker Hub: https://hub.docker.com/
   1. Create production-ready recipes for Kubernetes ```ansible-container shipit kube --save-config```
   1. Create services: ```kubectl create -f ansible/shipit_config/kubernetes/```
   1. Get pods information: ```kubectl get pods```
   1. Notice how application and database images has been pulled from Docker Hub repository.
   1. Get instance information (Your instance ID will differ slightly): ```kubectl describe pod wordpress-...```
   1. Get services information: ```kubectl get service wordpress```
   1. Connect to the external IP of your wordpress (either with ssh dynamic port forwarding or plain ```curl -sL```)
1. Once complete cleanup your lab environment: ```az group delete --name ... --yes```
1. Try other examples by yourself, explore, research and... have fun!

### References

- http://alesnosek.com/blog/2016/09/12/first-impressions-about-ansible-container/
- https://github.com/ansible/ansible-container-examples/tree/master/wordpress
- https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

## BUGS

- [x] 0.9.0.0 has breaking changes, reverted to 0.3.0 [https://github.com/ansible/ansible-container/issues/448]

