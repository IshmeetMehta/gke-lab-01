## gke-lab-01

#Gcloud commands

gcloud config set compute/region us-central1

gcloud config set compute/zone us-central1-a

#Source code

git clone https://github.com/IshmeetMehta/gke-lab-01.git

#Docker commands

docker build -t gcr.io/$DEVSHELL_PROJECT_ID/hello-lab-v1 .

docker images

gcloud auth configure-docker

docker push gcr.io/$DEVSHELL_PROJECT_ID/hello-lab-v1

gcloud container clusters create  hello-cluster

gcloud container clusters get-credentials hello-cluster

#Create deployment

kubectl create deployment hello-lab --image=gcr.io/$DEVSHELL_PROJECT_ID/hello-lab-v1
kubectl expose deployment hello-lab --type=LoadBalancer --port 80 --target-port 80

#Publish Service

kubectl get service

#Publish version 2 of service

docker build -t gcr.io/$DEVSHELL_PROJECT_ID/hello-lab-v2 .
docker push gcr.io/$DEVSHELL_PROJECT_ID/hello-lab-v2

kubectl edit deployment.v1.apps/hello-lab

kubectl set image deployment/hello-lab hello-lab-v1=gcr.io/$DEVSHELL_PROJECT_ID/hello-lab-v2

kubectl autoscale deployment hello-lab --max 6 --min 4 --cpu-percent 50
gcloud container clusters resize hello-cluster -size 3


gcloud containers clusters update hello-cluster --enable-autoscaling --min nodes 2 --max-nodes 8

# Check the logs for pods

Kubectl logs <POD_ID>

