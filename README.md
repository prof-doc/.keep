# .keep

# setting up to run makefile to run from any directory

Add the following to .bashrc
```
alias makeg='make -c <path to make file> --silent'
```
Use makeg to run any function you want such as 
```
makeg create-cluster
```
