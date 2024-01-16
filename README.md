# kubernetes

- Installations
  - curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  - sudo install minikube-linux-amd64 /usr/local/bin/minikube
  - sudo chmod +x /usr/local/bin/minikube
  - minikube start

  - sudo apt-get update && sudo apt-get install -y kubectl
  <!-- or run this command: sudo snap install kubectl -->
  - kubectl cluster-info
  - kubectl get nodes
  - kubectl version --client <!-- to check installed kubectl -->

- Deployments
  - `Docker build -t node-app`
  - `minikube start`
  - `minikube status`
  now create repo on docker hub by name **kub-node-app** :
  - `docker tag node-app amitreddy/kub-node-app`
  - `docker push amitreddy/kub-node-app`
  now deploy docker image on kubectl:
  - `kubectl create deployment first-app --image=amitreddy/kub-node-app`
  check deployments:
  - `kubectl get deployments`
  - `kubectl get pods`
  To see deployments:
  - `minikube dashboard`
  To Expose deployments with a service
  - `kubectl expose deployment first-app --type=LoadBalancer --port=8080`
  - `kubectl get services`
  - `minikube service kub-node-app`
  To scale the deployments:
  - `kubectl scale deployment/kub-first-node-app --replicas=3`
  - `kubectl get pods`

