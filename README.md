# Kubernetes tutorial

## Following by this tutorial:
https://www.youtube.com/watch?v=d6WC5n9G_sM

## This tutorial setup a simple node js webserver to docker by Dockerfile, push it to Docker Hub and control it in Kubernetes by command or file .yaml

1. Build and Push image to docker hub
`docker build . -t saxsax199502a/k8s-web-hello`
`docker login`
`docker push saxsax199502a/k8s-web-hello`
2. Create deployment based on the image that we just push to docker hub
`kubectl create deployment k8s-web-hello --image=saxsax199502a/k8s-web-hello`
3. Expose the webserver
`k expose deployment k8s-web-hello --port=3000`
4. Access to webserver by curl
`minicube ssh`
`curl 10.107.54.30:3000; echo`
5. Scale up the deployment
`kubectl scale deployment k8s-web-hello --replicas=4`

Now, whenever we curl to the webserver, it will run to difference replicas (which we called load balancer)
`curl 10.107.54.30:3000; echo`
6. Expose the webservice to the outside word
`kubectl delete service k8s-web-hello`
`k expose deployment k8s-web-hello --type=NodePort --port=3000`
`minikube ip`

Now we can access to webserver through web browswer
`http://192.168.49.2:32267/`
7. Change content of `index.mjs` and push it on docker hub and update deployment based on the image that we just push to docker hub
`kubectl set image deployment k8s-web-hello k8s-web-hello=saxsax199502a/k8s-web-hello:2.0.0`
`kubectl rollout status deployment k8s-web-hello`

Now we can access to webserver through web browswer and see the change have been applied
`http://192.168.49.2:30857/`
8. Rollback the change
`kubectl set image deployment k8s-web-hello k8s-web-hello=saxsax199502a/k8s-web-hello`
`kubectl rollout status deployment k8s-web-hello`

Now we can access to webserver through web browswer and see the change have been rollback
`http://192.168.49.2:30857/`
9. Delete all the resouce so we can re-build it by using .yaml file
`kubectl delete all --all`
10. Install kubenetes by .yaml file

Install Kubenetes extension on visual studio.

Create file deployment.yaml, type "Deployment" and Kubenetes extension will suggest you to use their template.

Do this also for service.yaml file
9. Delete one more time all the resouce
`kubectl delete all --all`
11. Combine deployment.yaml and service.yaml to a file called k8s-web-to-nginx.yaml

We gonna use that k8s-web-to-nginx.yaml to create another k8s deployment and service for k8s-web-to-nginx folder

Do the same for nginx
