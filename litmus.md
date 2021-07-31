### Install the Chaos Operator
kubectl apply -f https://litmuschaos.github.io/litmus/litmus-operator-v1.13.8.yaml


### Helm 
helm repo add litmuschaos https://litmuschaos.github.io/litmus-helm/
kubectl create ns litmus
helm install chaos litmuschaos/litmus --namespace=litmus


### check
kubectl get pods -n litmus
kubectl get crds | grep chaos
kubectl api-resources | grep chaos


### Install the Chaos Experiment 
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.13.8?file=charts/generic/pod-delete/experiment.yaml

### see all available chaos experiments
kubectl get chaosexperiments

### Setup service account
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.13.8?file=charts/generic/pod-delete/rbac.yaml

### Inject chaos
kubectl apply -f litmus/delete-engine.yaml

### Descrive chaosengine
kubectl get chaosengine
kubectl describe chaosengine bookinfo-chaos

### View result
kubectl get chaosresults
kubectl describe chaosresults bookinfo-chaos-pod-delete


### Inject chaos with probe
kubectl apply -f litmus/delete-engine-with-probe.yaml


### Check result

### Increase replica for productpage
kubectl scale deployments/productpage-v1 --replicas=5


### Install ALL generic experiments
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.13.8?file=charts/generic/experiments.yaml


kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.13.8?file=charts/generic/pod-network-latency/rbac.yaml
kubectl apply -f litmus/delay-engine.yaml


http://details:9080/details/1

http://localhost:9080/api/v1/products/1