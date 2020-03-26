# netjs-kubernetes

## Steps to deploy nest js application on kubernetes.

- Download Docker tool box or Docker Desktop 
  Download Docker tool box from [https://docs.docker.com/toolbox/toolbox_install_windows/]
  OR
  if you have Windows Pro / Enterprise Download Docker Desktop for Windows.
  https://docs.docker.com/docker-for-windows/

- Create Docker file on path where your package.json file is:
```
FROM node:12 AS builder
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build


FROM node:12-alpine
WORKDIR /app
COPY --from=builder /app ./
EXPOSE 3000
CMD ["npm", "run", "start:prod"]
```

- Install Kubectl
  ```
  choco install kubectl
  ```
- Install Minikube
  ```
  choco install minikube
  ```
- Create a file named prodapp.deployment.yml
  ```
- Start Minikube
  ```
  minikube start
  ```
- Change Minikube docker Environment, if docker is already started.
  ```
  minikube docker-env | Invoke Expression
  ```
- Build docker image 
  ```
  docker build -t prodapp:v1 .
  ```
- Initiate deployment pod
  ```
  kubectl apply -f prodapp.deployment.yml
  ```
- Check status of deployment
  ```
  kubectl get deployments
  ```
  If all deployments are running.

- Expose deployments to Loadbalancer service directly.
  ```
  kubectl expose deployment prodappnew-deployment --type="LoadBalancer"
  ```
- Get url of load balancer
  ```
  # netjs-kubernetes

## Steps to deploy nest js application on kubernetes.

- Download Docker tool box or Docker Desktop 
  Download Docker tool box from [https://docs.docker.com/toolbox/toolbox_install_windows/]
  OR
  if you have Windows Pro / Enterprise Download Docker Desktop for Windows.
  https://docs.docker.com/docker-for-windows/

- Create Docker file on path where your package.json file is:
```
FROM node:12 AS builder
WORKDIR /app
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build


FROM node:12-alpine
WORKDIR /app
COPY --from=builder /app ./
EXPOSE 3000
CMD ["npm", "run", "start:prod"]
```

- Install Kubectl
  ```
  choco install kubectl
  ```
- Install Minikube
  ```
  choco install minikube
  ```
- Create a file named prodapp.deployment.yml
  ```
- Start Minikube
  ```
  minikube start
  ```
- Change Minikube docker Environment, if docker is already started.
  ```
  minikube docker-env | Invoke Expression
  ```
- Build docker image 
  ```
  docker build -t prodapp:v1 .
  ```
- Initiate deployment pod
  ```
  kubectl apply -f prodapp.deployment.yml
  ```
- Check status of deployment
  ```
  kubectl get deployments
  ```
  If all deployments are running.

- Expose deployments to Loadbalancer service directly.
  ```
  kubectl expose deployment prodapp-deployment --type="LoadBalancer"
  ```
- Get load balancer url
  ```
  minikube service prodapp-deployment --url
  ```
- run url in browser/postman to get expected output
