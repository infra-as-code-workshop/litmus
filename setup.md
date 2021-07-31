## STEP 1: Install Docker for Desktop

## STEP 2: Install k3d
brew install k3d

## STEP 3: Create Kubernetes Cluster (using K3D locally)
k3d cluster create default --agents 3 --image docker.io/rancher/k3s:v1.21.3-k3s1
 
## STEP 4: Deploy Book Info application
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.10/samples/bookinfo/platform/kube/bookinfo.yaml

## STEP 5: port forwarding
kubectl port-forward service/productpage 9080:9080

## STEP 6: Verify
http://localhost:9080/productpage?u=normal

## STEP 7: Stop your clust (DO NOT DELETE)
k3d cluster stop default


===========================

## to start your cluster
k3d cluster start default

## log inside worker node 
docker exec -it k3d-default-agent-1 /bin/sh

## get all nodes
kubectl get nodes -o wide

