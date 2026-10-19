
# Lab 10: Multi-Node Kubernetes Deployment

## Aim
To deploy multiple applications with replicas on a three-node Minikube cluster.

## Applications
1. Product Catalog - 2 replicas
2. Shopping Cart - 3 replicas

## Technologies Used
- Python and Flask
- Docker
- Kubernetes
- Minikube
- YAML
- Git and GitHub

## Project Structure
- product_catalog.py
- shopping_cart.py
- Dockerfile.product
- Dockerfile.shopping
- product_catalog_deployment.yaml
- shopping_cart_deployment.yaml
- product_catalog_service.yaml
- shopping_cart_service.yaml

## Steps to Execute

### 1. Start Minikube
```bash
minikube start --nodes 3 -p devops-multinode --driver=docker
```

### 2. Build Docker Images
```bash
docker build -t product-catalog:latest -f Dockerfile.product .
docker build -t shopping-cart:latest -f Dockerfile.shopping .
```

### 3. Load Images into Minikube
```bash
minikube -p devops-multinode image load product-catalog:latest
minikube -p devops-multinode image load shopping-cart:latest
```

### 4. Create Namespace
```bash
kubectl create namespace devops-exercise
```

### 5. Deploy Applications
```bash
kubectl apply -f product_catalog_deployment.yaml
kubectl apply -f shopping_cart_deployment.yaml
```

### 6. Create Services
```bash
kubectl apply -f product_catalog_service.yaml
kubectl apply -f shopping_cart_service.yaml
```

### 7. Verify Pods
```bash
kubectl get pods -A -o wide
```

### 8. Access Services
```bash
minikube -p devops-multinode service product-catalog-service
minikube -p devops-multinode service shopping-cart-service -n devops-exercise
```

## Expected Result
Five application pods should run across the three nodes:
- 2 Product Catalog pods
- 3 Shopping Cart pods

## Conclusion
Both applications are deployed on a multi-node Kubernetes cluster with replicas to improve availability and fault tolerance.
