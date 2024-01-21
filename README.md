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
