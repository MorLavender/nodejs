# nodejs
simple nodejs app 

Node App
--------
1. Create an empty node package: npm init -y
2. Install express as a dependency: npm install express
3. index.js
  
  
Docker
------
1. Dockerfile

FROM node:13-alpine

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install --production

COPY . .

EXPOSE 3000

CMD node index.js
 
2.Build the image: docker build -t mmichaeli/node-hello-app .
3.Edit index.js and replace the word Hi with Hello.
4.Re-build the image and notice Docker re-using previous layers: docker build -t mmichaeli/node-hello-app .
5.Run a container to test it: docker run --rm -d -p 3000:3000 mmichaeli/node-hello-app
6.Look at the running containers: docker ps
7.Stop the container: docker stop CONTAINER_ID
8.Push the image to DockerHub: docker push mmichaeli/node-hello-app



Kubernetes
----------
Get worker nodes: kubectl get nodes
Create a deployment: kubectl create deployment --image kamaln7/node-hello-app node-app
Scale up to 3 replicas: kubectl scale deployment node-app --replicas 3
Expose the deployment as a NodePort replica: kubectl expose deployment node-app --type=NodePort --port 3000
Look at the newly created service (and the assigned port): kubectl get services
Grab the public IP of one of the worker nodes: kubectl get nodes -o wide
Browse to IP:port to test the service
Edit the service: kubectl edit service node-app
Replace port: 3000 with port: 80
Replace type: NodePort with type: LoadBalancer
Verify that the service was updated: kubectl get service
Run the above command every few seconds until you get the external IP address of the Load Balancer
Browse to the IP of the Load Balancer


