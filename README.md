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
