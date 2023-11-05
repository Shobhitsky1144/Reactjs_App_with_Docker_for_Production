# React + TypeScript + Vite

STEP 1 => DOCKER FILE

# Dockerfile

FROM node:alpine3.16 as nodework

WORKDIR /myapp

COPY package.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:1.23-alpine

WORKDIR /usr/share/nginx/html 

RUN rm -rf ./*

COPY --from=nodework /myapp/dist /usr/share/nginx/html

ENTRYPOINT ["nginx", "-g", "daemon off;"]

STEP 2==> docker build -t react-production-img .

STEP 3==> docker run --name react-production-container -p 3000:80 react-production-img


===================DOCKER COMPOSE FOR PRODUCTION ================

STEP 1=> DOCKER-COMPOSE.YML:

version: "3"

services:

  web:
  
    build: .
    
    container_name: vite_docker
    
    ports:
    
      - 8080:80

STEP 2=> docker compose up
