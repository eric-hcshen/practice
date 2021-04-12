# Install mySQL on K8S Kind

## Reference
[Setting up a Standalone MYSQL Instance on Kubernetes & exposing it using Nginx Ingress Controller](https://chrisedrego.medium.com/setting-up-a-standalone-mysql-instance-on-kubernetes-exposing-it-using-nginx-ingress-controller-262fc7af593a)
[Run a Single-Instance Stateful Application](https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/)
[Setting up an ingress controller](https://kind.sigs.k8s.io/docs/user/ingress/)
[Pull imae to Kind](https://ithelp.ithome.com.tw/articles/10241682)
- Create Kind cluster
> kind create cluster --config kind.yaml

````yaml
cat <<EOF | kind create cluster --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
  extraPortMappings:
  - containerPort: 80
    hostPort: 80
    protocol: TCP
  - containerPort: 443
    hostPort: 443
    protocol: TCP
  - containerPort: 3316
    hostPort: 3316
    protocol: TCP
EOF
````

- Load image from docker to Kind
> kind load docker-image  mysql:5
- Check image has been ready in Kind CRI (Container Runtime Interface)
> docker exec -it kind-worker crictl image
- Create namespace
> kubectl create ns mysql
- Create secret
> kubectl create -f my-secret.yaml
- Create configMap
> kubectl create -f mysql-config.yaml
- Create PVC
> kubectl create -f mysql-pvc.yaml 
- Create deployment
> kubectl create -f mysql-deployment.yaml 
- Create service
> kubectl create -f mysql-service-headless.yaml
- Attached to running MySQL
> Kubectl -n mysql -it exec mysql-7474c766c6-pdl9m /bin/bash
- Connect mySQL
> kubectl -n mysql run -it --rm --image=mysql:5 --restart=Never mysql-client -- mysql -h mysql -ppassword

