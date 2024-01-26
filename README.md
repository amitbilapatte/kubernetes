# KUBERNETES

## Installations

- `curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
- `sudo install minikube-linux-amd64 /usr/local/bin/minikube`
- `sudo chmod +x /usr/local/bin/minikube`
- `minikube start`

- `sudo apt-get update && sudo apt-get install -y kubectl`
  <!-- or run this command: sudo snap install kubectl -->
- `kubectl cluster-info`
- `kubectl get nodes`
- `kubectl version --client` <!-- to check installed kubectl -->

## Deployments

- `Docker build -t node-app`
- `minikube start`
- `minikube status`
- `minikube stop`

  *now create repo on docker hub by name **kub-first-app** :*

- `docker tag node-app amitreddy/kub-first-app`
- `docker push amitreddy/kub-first-app`

  *now deploy docker image on kubectl:*

- `kubectl create deployment first-app --image=amitreddy/kub-first-app`

  *check deployments:*

- `kubectl get deployments`
- `kubectl get pods`

  *To see deployments:*

- `minikube dashboard`

  *To Expose deployments with a service:*

- `kubectl expose deployment first-app --type=LoadBalancer --port=8080`<!-- expose port number  & specify load balancer for distributing load evenly across all pods(containers) ->
- `kubectl get services`
- `minikube service kub-first-app` <!-- it will show port number for deplyed service and also rdirect to this service on browser-->

  *To scale the deployments:*

- `kubectl scale deployment/kub-first-app --replicas=3` <!-- increase pods(containers) replicas to 3 to manage traffic ->
- `kubectl get pods`

  *To delete the deployments:*

- `kubectl delete service kub-first-app`
- `kubectl get pods`

  *To Update the deployments:*
- rebuild the image with new tag/version `docker build -t amitreddy/kub-first-app:2 .`
- check deployment is still there `kubectl get deployment`
- push image to docker hub `docker push amitreddy/kub-first-app:2`
- update deployment image `kubectl set image deployment/first-app kubernetes-node-app=amitreddy/kub-first-app:2` 
  `kubernetes-node-app` is the image name you can find in pods whose image is to be updated in minikube dashboard
- now roll out this deployment to see changes `kubectl rollout status deployment/first-app`
- `kubectl delete service kub-first-app`
- `kubectl get pods`

  *To Update the deployments:*
- update deployment image with tag/version that doesn't exist so that it fails `kubectl set image deployment/first-app kubernetes-node-app=amitreddy/kub-first-app:3`
- check status of new rollout`kubectl rollout status deployment/first-app`
  here old pod doesn't shut down till new pod deployment is successfully deployed. so it will never succeed as we have entered image name tag that doesn't exist.
- to check this `kubectl get pods` it will show "ImagePullBackOff" status for new deployment. and it fails.
- To rollback this deployment to previous deployment `kubectl rollout undo deployment/first-app`
- To go back to older deployment :
  - `kubectl rollout history deployment/first-app` it will list down all revisions for this deployment
  - To see details about a partucular revision: `kubectl rollout history deployment/first-app --revision=3`
  - To go back to specific revision `kubectl rollout undo deployment/first-app --to-revision=1` here 1 is revision number we want to roll back to.

## Deployment Using .yaml file

- create a **deployment.yaml** file
- deploy this file using command `kubectl apply -f=deployment.yaml`
- check deployment using `kubectl get deployments` && `kubectl get pods`
