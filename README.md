# minikube-project
For learning a minikube project
download and install minikube

https://kubernetes.io/docs/tasks/tools/install-kubectl/
https://github.com/kubernetes/minikube
https://minikube.sigs.k8s.io/docs/start/

if you are using minikube in vm you've to install conntrack and start kube by typing
$ sudo minikube start --driver=none

download all file content of minikube file .
you can cat server.js and Dockerfile to see the content.
Now we've to tell minikube which docker enviornmnet to use type :

$ eval $(minikube docker-env)

Now we are ready to build our countainer by typing 

$ docker build -t hello-node:v1 . { don't foget the dot in the end of command }

all right our container is ready to go !! now we'll deploy our container in kubernaties and use kubectl to interact with minikube cluster

$kubectl run hello-node --image=hello-node:v1 --port=8080

This will create both deployment and the pod . And deploymnet is created and we can use kubectl to interact with that as well

$ kubectl get deployments 

And there is hello node and it looks like everything is ready . And you can also use kubectl to list out the pod.

$ kubectl get pods

Right now our pod is only accessible inside the cluster though. Let's create a service and expose it and we will give it a type load balancer  which makes it available outward . by typing below command you can see that our service is up and ready.

$ kubectl expose deployment hello-node --type=loadBalancer

list services 

$kubectl get services

now type 

$minikube service hello-node 

this will open your browser where our service is running .

$minikube dashboard

It will open dashboard under workload , where we can see details about our deployment and pods . ( more kubernates.io ) 

----------------------------------------

Now lt's have some orchestration !!
go to the nginx directory and cat the deployment.yaml file . you can see that it will start two pods deployment of nginx. 
our deployment model specifies two replicas and points to the nginx1.79 container as the source .

Now lets get out deployment all set up .

$kubectl create -f deployment.yaml 

Let's list out the pods , we've two of nginx pods are ready to go !!

$ kubectl get pods

we have deployment dash update.yaml file , this file tells kubernetes we want to move to sex replicas and upgrade to nginx 1.8. let's do that .
Once we apply the new model specification kubernates does a rolling upgrade and make sure that the cluster now meets the new spec.

$ kubectl apply -f deployment-update.yaml

Now , our new deployment mode is ready to go .  Now our new pods are comming online we can list our pods by

$ kubectl get pods

see there are 6 nginx pods ready to go . Also we go to the UI and update our deployment straight from there. let's double down our deployment to 12 replicas

$minikube dashboard

go to workloads > deployments > three dots click >  view/edit yaml > in the file under SPEC -> relicas form 6 to 12 | and click update \\

# Now go to docs or explore , do whatever you like to  do with dashboard do some expriment !! 






