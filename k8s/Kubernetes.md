# Kubernetes

## ReplicaController/ReplicaSets

````yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-1
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx
````

>kubctl create -f rc-definition.yml
>kubctl get replicacontroller
>kubctl get replicaset.apps
>kubctl delete replicaset myapp-replicaset
>kubctl get pods
>kubctl replace -f replicast-definition.yml
>kubctl scale --replicas=6 replicaset-difnition.yml
>kubctl describe replicasets.apps [name of replicaset]
>kubctl edit replicasets.apps new-replica-set


## Deployment

>kubctl get all

## Namespace

Within the same namespace
> mysql.connect('db-service')

Out of local namespace
> mysql.connect('db-service.dev.svc.cluster.local') <=DNS name of service. cluster.local is domain name. The convention is service name + namespace + service + domain

Get pod out of default namespace
> kubectl get pods --namespace=kube-system

Stick on specific namespace
> kubectl config set-contect $(kubectl config current-contect) --namespace=dev

Get pad in all namespace
> kubectl get pods --all-namespaces

Create an NGINX Pod
> kubectl run nginx --image=nginx

Create POD Manifest YAML (-o yaml). Don't create it(--dry-run)
> kubectl run nginx --image=nginx --dry-run=client -o yaml

Create a deployment
> kubetl create deployment --image=nginx nginx

Create a service
> kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
> kubectl expose pod redis --name redis-service --port 6379 --target-port 6379
> kubectl run httpd --image=httpd:alpine --port=80 --expose

## Configuration

### Create ConfigMaps
> kubectl create configmap \
>   app-config --from-literal=APP_COLOR=blue \
>              --from-literal=APP_MOD=prod

>kubectl create configmap app-config --from-file=app_config.properties

config-map.yaml
````yaml
apiVersion: v1
Kind: ConfigMap
metadata:
   name: app-config
data:
   APP_COLOR: blue
   APP_MODE: prod
````

````yaml
spec:
   containers:
   - envFrom:
     - configMapRef:
         name: app-config
````

### Create Secret

secret-data.yaml
````yaml
apiVersion: v1
kind: Secret
metadata:
   name: app-secret
data:
   DB_HOST:
   DB_User:
   DB_Password:

````

````yaml
apiVersion: v1
kind: Pod
metadata:
   name: simple-webapp-color
   labels:
      name: sime-webapp-color
spec:
   containers:
   - name: simple-webapp-color
     image: simple-webapp-color
     ports:
       - containerPort: 8080
     eveForm:
       - secretRef:
          name: app-secret
````