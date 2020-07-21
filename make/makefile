use-registry := $(for node in $(kind get nodes --name standard); do,kubectl annotate node "${node}" "kind.x-k8s.io/registry=localhost:5000";,done)

help:
	@echo "Run 'makeg start-cluster' to create kind cluster with LB"
	@echo "Run 'makeg delete-cluster' to dekete kind cluster with LB"


create-cluster:
	@echo "Creating local registry"
	@docker run -d --restart=always -p 5000:5000 --name kind-registry registry:2
	@kind create cluster --name standard --config ../kind-config/cluster-config.yaml
	@kubectl get configmap kube-proxy -n kube-system -o yaml | sed -e "s/strictARP: false/strictARP: true/" | kubectl apply -f - -n kube-system
	@kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/namespace.yaml
	@kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/metallb.yaml
	@kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
	@kubectl apply -f ../kind-config/metal-lb-config.yaml
	@docker network connect "kind" kind-registry
	@$(use-registry)
	@echo "\nTo use the registry pull the image and the tag it to use local registry using"
	@echo "docker tag <image> localhost:5000/<image>"
	@echo "docker push localhost:5000/<image>"

delete-cluster:
	@kind delete cluster --name standard
	@docker stop kind-registry
	@docker rm kind-registry
