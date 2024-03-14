v15

elastic basic auth no https just http
elasticsearch keeps sensitive info in /usr/share/elasticsearch/config
elasticsearch.keystore is stored in this path.

elastic keeps the password for the "elastic" user in its internal database, if you have persistent volume for data directory
then no problem /usr/share/elasticsearch/data

kafka stuff:

for bitnami images use the ones with r tag

kafka data directory for persistent volume /bitnami/kafka

kafka sh scripts directory /opt/bitnami/kafka/bin



---
v14

n8n - no pv
bitnami kafka - no pv
redis - no pv
elastic - no pv

---
v13

confluent kafka &  confluent zookeeper & n8n

counfluentinc/kafka
counfluentinc/zookeeper

#bu linklere bakmadan zor
https://docs.confluent.io/platform/current/installation/docker/config-reference.html#cp-kakfa-example
https://docs.confluent.io/platform/current/installation/docker/config-reference.html#zk-config

kubectl apply -f zookeeper-deployment.yml
kubectl apply -f zookeeper-service.yml
kubectl apply -f kafka-deployment.yml
kubectl apply -f kafka-service.yml
kubectl apply -f n8n-deployment.yml
kubectl apply -f n8n-service.yml

---
v10

CHECK VOLUME STUFF FOR n8n-worker-deployment !!!

n8n
    execution process own
    execution mode queue
    PERSISTENT

postgres
    PERSISTENT

redis
    PERSISTENT

to be able to connect to kafka running on host, from k8s n8n:
on the host machine
 >ip addr =>

find the one with 192.168.xx

and set kafka's server.properties file

#CUSTOM_BY_ME
listeners = PLAINTEXT://192.168.49.1:9092

use this url on n8n kafka credential

minikube ssh => create required directories
  >pwd
  /home/docker
  >mkdir kubey
  >cd kubey
  >mkdir postgres-storage
  >mkdir n8n-storage
  >mkdir redis-storage
  >mkdir elastic-storage
  >sudo chmod 777 elastic-storage
  >mkdir kibana-storage
  >sudo chmod 777 kibana-storage

kubectl apply -f devam-volume.yml
kubectl apply -f postgres-deployment.yml
kubectl apply -f postgres-service.yml
kubectl apply -f n8n-deployment.yml
kubectl apply -f n8n-worker-deployment.yml
kubectl apply -f n8n-service.yml
kubectl apply -f redis-deployment.yml
kubectl apply -f redis-service.yml
kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml
kubectl apply -f kibana-deployment.yml
kubectl apply -f kibana-service.yml

---
v9

CHECK VOLUME STUFF FOR n8n-worker-deployment !!!

n8n
    execution process own
    execution mode queue
    postgres NOT PERSISTENT YET!!!

to be able to connect to kafka running on host, from k8s n8n:
on the host machine
 >ip addr =>

find the one with 192.168.xx

and set kafka's server.properties file

#CUSTOM_BY_ME
listeners = PLAINTEXT://192.168.49.1:9092

use this url on n8n kafka credential

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
kubectl apply -f postgres-deployment.yml
kubectl apply -f postgres-service.yml
kubectl apply -f n8n-deployment.yml
kubectl apply -f n8n-worker-deployment.yml
kubectl apply -f n8n-service.yml
kubectl apply -f redis-deployment.yml
kubectl apply -f redis-service.yml
kubectl apply -f elastic-config.yml
kubectl apply -f elastic-deployment.yml
kubectl apply -f elastic-service.yml
kubectl apply -f kibana-deployment.yml
kubectl apply -f kibana-service.yml

---
v8

to be able to connect to kafka running on host, from k8s n8n:
on the host machine
 >ip addr =>

find the one with 192.168.xx

and set kafka's server.properties file

#CUSTOM_BY_ME
listeners = PLAINTEXT://192.168.49.1:9092

use this url on n8n kafka credential

n8n
    execution process own
    execution mode regular
    sqlite

---
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


