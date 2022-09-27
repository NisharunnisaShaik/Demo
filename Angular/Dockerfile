### STAGE 1: Build ###
FROM node:14.20.0-alpine3.16 AS build
WORKDIR /usr/src/app
COPY package.json package-lock.json ./
RUN npm config set ca ""
RUN npm config set strict-ssl false
RUN npm install
RUN npm audit fix 
RUN npm install -g @angular/cli
COPY . .
RUN ng build

### STAGE 2: Run ###
FROM nginx:1.22.0-alpine
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /usr/src/app/dist /usr/share/nginx/html

