v3

elasticsearch works, no persistence

kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml

only elastic tested in this version

elastic-config.yml overrides existing elastic default configuration, edit it if you need to add/remove something
---

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


