# .keep

The following repo contain files to create a kind cluster with a single control
pane node and 2 worker nodes.

Metallb has also been implimented for a local loadbalancer. You may need to
change the ip in the config for the lb to work. To do this run the following
commands
```
ip addr show
```
Use the ip output to get the ip used by docker. Update metal-lb-config.yaml
found
```
.keep/kind-config/metal-lb-config.yaml
```
with the ip found. Example below
```
172.18.255.1-172.18.255.250
```

Along with this a local repo is also created with the kind cluster. You can
access the cluster using http://localhost:5000

you can push and pull any image to the repo while testing. 

*****************Note: The repo will be deleted when the cluster is delete**

# setting up to run makefile to run from any directory

Add the following to .bashrc
```
alias makeg='make -c <path to repo>/.keep/make --silent'
```
Use makeg to run any function you want such as 
```
makeg create-cluster
```

# Adding the scripts to path

Add the following to your.bashrc
```
export PATH=$PATH:<path to repo>/.keep/script
```
You can then run the scripts by calling the script as such
```
create-cluster
```
