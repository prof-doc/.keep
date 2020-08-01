# .keep

The following repo contain files to create a kind cluster with a single control
pane node and 2 worker nodes.

Metallb is also implemented for a local loadbalancer. You will need to set a ip
range to be load used. By default docker uses 172.17.0.1/16 address block. Edit the following file
```
.keep/kind-config/metal-lb-config.yaml
```
To use the following range 172.17.255.1-172.17.255.250
Uncomment line 12 to use the default range and comment out line 13. If docker
is using a different ip block then run the following commands 
```
ip addr show
```
Set the range in the file stated above.

Along with this a local registry is also created with the kind cluster. You can
access the cluster using http://localhost:5000

you can push and pull any image to the repo while testing. 

__Note: Deleting the cluster will also delete the private repo__


**It is recomended to use the scripts over the makefile. The makefile is just
a example of one use use can use this repo**
# Setting up to run makefile to run from any directory

Add the following to .bashrc
```
alias makeg='make -c <path to repo>/.keep/make --silent'
```
Use makeg to run any function you want such as 
```
makeg create-cluster
```

**Note using this method will delete the private registry**
# Adding the scripts to path

Add the following to your.bashrc
```
export PATH=$PATH:<path to repo>/.keep/script
```
You can then run the scripts by calling the script as such
```
create-cluster
```

**The private registry will be created if it does not exsist.**
