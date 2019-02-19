# Election

## What is Election?
- Election is simple voting web application I created to explore microservices architecture. This was also a good handson exercise for creating containers and orchestrating them using Kuberenetes. Each component of the web-app is dockerized and converted to a microservice
- All the microservices are then deployed on Google Kuberenetes Engine and scaled independently.

## Architecture
![Architecture](https://github.com/aborse3/election/blob/master/archi.png)

## How it works?
- Client selects his/her vote on the Select_lb service. This service is nothing but the load-balancer , which balances the load among all the select PODs
- Select PODs then saves the vote of the client in the REDIS cache, and respond to the client with success.
- COPY Deamon POD contains the daemon to transfer the vote from REDIS cache to Postgresql DB.
- When client visits the result_lb ( load balancer service endpoint) request is fullfilled by Result PODS. One of the result POD queries on the Postgresql db and returns the vote count.

## How to use?
- Go to Google Kuberenetes Engine and create a Kuberenetes cluster.
```bash
gcloud container clusters create mycluster1
```
- Create a namespace
```bash
kubectl create namespace thisorthat
```
- Clone this repository
- Deploy using manifests
```bash
kubectl create -f kuberenetesYAML
```
- Get the endpoint and ports to vote on the select UI and check the results on result UI
```bash
kubectl describe services --namespace=thisorthat
```
