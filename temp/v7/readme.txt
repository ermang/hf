v7

general cleanup

minikube ssh => create required directories
  >pwd
  /home/docker
  >mkdir kubey
  >cd kubey
  >mkdir n8n-storage
  >mkdir redis-storage
  >mkdir elastic-storage
  >sudo chmod 777 elastic-storage
  >mkdir kibana-storage
  >sudo chmod 777 kibana-storage

kubectl apply -f devam-volume.yml
kubectl apply -f n8n-deployment.yml
kubectl apply -f n8n-service.yml
kubectl apply -f redis-deployment.yml
kubectl apply -f redis-service.yml
kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml
kubectl apply -f kibana-deployment.yml
kubectl apply -f kibana-service.yml
---
v6

elastic works + persistence works
kibana works + persistence works

kibana-deployment.yml da

ev:
  ELASTICSEARCH_HOSTS => bunu setlemek gerekiyor, kibana yi kaldirmadan once. sonra kubectl apply -f kibana-deployment.yml

https://discuss.elastic.co/t/kibana-asking-for-enrollment-token-when-xpack-security-enabled-false-in-elasticsearch/302118

surdaki gibi olmasi lazim aslinda sadec 1. adimdaki gibi ama istedi illa ELASTICSEARCH_HOSTS u env den parametre olarak

minikube ssh => create required directories
  >pwd
  /home/docker
  >mkdir kubey
  >cd kubey
  >mkdir redis-storage
  >mkdir n8n-storage
  >mkdir elastic-storage
  >sudo chmod 777 elastic-storage
  >mkdir kibana-storage
  >sudo chmod 777 kibana-storage

kubectl apply -f devam-volume.yml
kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml
kubectl apply -f kibana-deployment.yml
kubectl apply -f kibana-service.yml

---
v5

elastic works + persistence works
kibana works + no persistence

minikube ssh => create required directories
  >pwd
  /home/docker
  >mkdir kubey
  >cd kubey
  >mkdir redis-storage
  >mkdir n8n-storage
  >mkdir elastic-storage
  >sudo chmod 700 elastic-storage

kubectl apply -f devam-volume.yml
kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml

---
v4
elasticsearch works, no auth no ssl, persistence works

minikube ssh => create required directories
  >pwd
  /home/docker
  >mkdir kubey
  >cd kubey
  >mkdir redis-storage
  >mkdir n8n-storage
  >mkdir elastic-storage
  >sudo chmod 700 elastic-storage

kubectl apply -f devam-volume.yml
kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml

---
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


