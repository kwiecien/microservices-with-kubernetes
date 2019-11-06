# UD615: Scalable Microservices with Kubernetes

This is the code for [Scalable Microservices with Kubernetes](https://www.udacity.com/course/scalable-microservices-with-kubernetes--ud615).  In this course you will learn how to:

* Provision a complete Kubernetes using [Google Container Engine](https://cloud.google.com/container-engine)
* Deploy and manage Docker containers using kubectl

Kubernetes Version: 1.2.2

## Course Description

Kubernetes is all about applications and in this course you will utilize the Kubernetes API to deploy, manage, and upgrade applications. In this part of the workshop you will use an example application called "app" to complete the labs.

App is an example [12 Factor application](http://12factor.net/) that we'll be using throughout the course. During this course you will be working with the following Docker images:

* [udacity/example-monolith](https://hub.docker.com/r/udacity/example-monolith) - Monolith includes auth and hello services.
* [udacity/example-auth](https://hub.docker.com/r/udacity/example-auth) - Auth microservice. Generates JWT tokens for authenticated users.
* [udacity/example-hello](https://hub.docker.com/r/udacity/example-hello) - Hello microservice. Greets authenticated users.
* [nginx](https://hub.docker.com/_/nginx) - Frontend to the auth and hello services.

## Links

  * [Kubernetes](http://googlecloudplatform.github.io/kubernetes)
  * [gcloud Tool Guide](https://cloud.google.com/sdk/gcloud)
  * [Docker](https://docs.docker.com)
  * [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
  * [nginx](http://nginx.org)

# Kubernetes - notes
 * gcloud config set compute/zone europe-west4-a
 * gcloud container clusters create k0
 * To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/europe-west4-a/k0?project=<PROJECT-ID>
 * kubectl run nginx --image=nginx:1.10.0
 * kubectl get pods
 * kubectl expose deployment nginx --port 80 --type LoadBalancer
 * kubectl create -f pods/monolith.yaml
 * kubectl describe pods monolith
 * kubectl port-forward monolith 10080:80
 * curl http://127.0.0.1:10080
 * kubectl logs -f monolith
 * kubectl exec monolith --stdin --tty -c monolith /bin/sh
 * ping -c 3 google.com
 * kubectl create -f pods/healthy-monolith.yaml
 * kubectl describe pods healthy-monolith | grep "Readiness"
 * kubectl describe pods healthy-monolith | grep "Liveness"
 * kubectl create secret generic tls-certs --from-file=tls/
 * kubectl describe secrets tls-certs
 * kubectl create configmap nginx-proxy-conf --from-file=nginx/proxy.conf
 * kubectl describe configmap nginx-proxy-conf
 * kubectl create -f pods/secure-monolith.yaml
 * kubectl get pods secure-monolith
 * kubectl port-forward secure-monolith 10443:443
 * curl --cacert tls/ca.pem https://127.0.0.1:10443
 * kubectl logs -c nginx secure-monolith
 
