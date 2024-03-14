n8n deployment
redis deployment
both use local-storage
for minikube:
  minikube ssh => create required directories
  >pwd
  /home/docker
  >mkdir kubey
  >cd kubey
  >mkdir redis-storage
  >mkdir n8n-storage


kubectl apply -f devam-volume.yml
kubectl apply -f devam-service.yml
kubectl apply -f redis-deployment.yml
kubectl apply -f devam-deployment.yml

when declaring redis credential, for the Host field use

{{ $env.CUSTOM_REDIS_HOST }}


