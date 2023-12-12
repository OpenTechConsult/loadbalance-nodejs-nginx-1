# loadbalance-nodejs-nginx-1

How to control the backend traffic of web application we serve using Nginx

This is a simple application that uses Nginx as a load balancer to control traffic comming from the client to node.js backend servers 

## Getting Started

To get started with this project you need to have docker installed on your system

1. Clone the repository

> git clone https://github.com/OpenTechConsult/loadbalance-nodejs-nginx-1.git

2. Navigate to the project directory

> cd loadbalance-nodejs-nginx-1

3. Navigate to the **server** directory

> cd server

4. build the image 

> docker built -t server .

5. create a network for all the future running containers to share.

>  docker network create loadbalance_net

6. run 4 containers as follow

> docker run -p 1010:5050 --name backend_server_1 -d --network loadbalance_net server

> docker run -p 2020:5050 --name backend_server_2 -d --network loadbalance_net server

> docker run -p 3030:5050 --name backend_server_3 -d --network loadbalance_net server

> docker run -p 4040:5050 --name backend_server_4 -d --network loadbalance_net server


7. After that cd into the nginx folder 

> cd nginx

8. Build the image inside the docker file

> docker build -t nginx_load_balancer .

9. run the nginx container 

> docker run -p 3000:80 --name nginx_server -d --network loadbalance_net nginx_load_balancer

10. You can the test our loadbalanced application by sending a request to http://localhost:3000

We will get a response saying

> This is the server's response