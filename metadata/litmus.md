## Install Metadata service
kubectl create namespace metadata 
kubectl apply -f metadata/metadata.yaml -n metadata
kubectl port-forward service/metadata 8080:8080  -n metadata

curl localhost:8080/metadata

curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"group":"sunitparekh","name":"city","value":"Pune"}' \
  http://localhost:8080/metadata

while true; do sleep 1; curl "localhost:8080/metadata"; echo -e '    '$(date);done


### Install the Chaos Operator
kubectl apply -f https://litmuschaos.github.io/litmus/litmus-operator-v1.12.0.yaml


### Helm 
helm repo add litmuschaos https://litmuschaos.github.io/litmus-helm/
kubectl create ns litmus
helm install chaos litmuschaos/litmus --namespace=litmus


### check
kubectl get pods -n litmus
kubectl get crds | grep chaos
kubectl api-resources | grep chaos

### Install the Chaos Experiment 
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.12.0?file=charts/generic/pod-delete/experiment.yaml

### see all available chaos experiments
kubectl get chaosexperiments

### Setup service account
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.12.0?file=charts/generic/pod-delete/rbac.yaml

### Inject chaos
kubectl apply -f metadata/pod-delete-engine.yaml

### Descrive chaosengine
kubectl describe chaosengine bookinfo-chaos

### View result
kubectl get chaosresults
kubectl describe chaosresults bookinfo-chaos-pod-delete


### Deploy metadata
kubectl apply -f metadata/metadata.yaml -n metadata

kubectl port-forward service/metadata 8080:8080

curl localhost:8080/metadata

curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"group":"sunitparekh","name":"city","value":"Pune"}' \
  http://localhost:8080/metadata



### Install ALL generic experiments
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.12.0?file=charts/generic/experiments.yaml

http://details:9080/details/1
http://localhost:9080/api/v1/products/1