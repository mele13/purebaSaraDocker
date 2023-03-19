# Stage 1: Compile and Build angular codebase
FROM node:16.18-alpine as build
#Accepting build-arg to create environment specific build
#it is useful when we have multiple environment (e.g: dev, tst, staging, prod)
#default value is development
ARG build_env=development
#Creating virtual directory inside docker image
WORKDIR /app
RUN npm cache clean --force
COPY package.json /app/package.json
RUN npm install
#Copying file from local machine to virtual docker image directory
COPY . /app
# Creating angular build
RUN ./node_modules/@angular/cli/bin/ng build --configuration=$build_env
# RUN npm run build --prod
# CMD ng serve

# Stage 2: Serve app with nginx server
FROM nginx:alpine
# Copy the build output to replace the default nginx contents.
COPY nginx.conf /etc/nginx/nginx.conf
COPY ./src/index.html /usr/share/nginx/html/
# Expose port 80 for HTTP traffic
EXPOSE 80
# daemon off runs nginx in the foreground
# CMD ["nginx", "-g", "daemon off;"]
