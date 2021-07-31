
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.12.0?file=charts/generic/experiments.yaml 
kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.12.0?file=charts/generic/pod-network-loss/experiment.yaml

kubectl apply -f https://hub.litmuschaos.io/api/chaos/1.12.0?file=charts/generic/pod-network-loss/rbac.yaml


kubectl get chaosexperiments
kubectl get chaosresults

kubectl describe chaosresults bookinfo-network-chaos-pod-network-loss



