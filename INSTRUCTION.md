Create the kind cluster from the provided config:
kind create cluster --name todoapp --config cluster.yml
Bootstrap the cluster (installs NGINX ingress controller and deploys the app):
chmod +x bootstrap.sh && ./bootstrap.sh
Apply the Ingress manifest (if not already applied by bootstrap):
kubectl apply -f ./.infrastructure/ingress/ingress.yml

kubectl get pods -o wide
kubectl describe pod $(kubectl get pod -l app=todoapp -n todoapp -o jsonpath='{.items[0].metadata.name}')
kubectl get nodes -o jsonpath="{range .items[*]}{.metadata.name} {.spec.taints[]}{\"\n\"}"
kubectl get nodes --show-labels
http://localhost:30007/