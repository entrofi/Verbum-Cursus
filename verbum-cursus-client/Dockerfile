FROM node:10.11.0-alpine as node

RUN apk update && apk add --no-cache make git


RUN mkdir /usr/app
WORKDIR /usr/app

COPY package.json package-lock.json  /usr/app/

RUN cd /usr/app && npm set progress=false && npm install


# Copy application files & build with npm
COPY . /usr/app
RUN cd /usr/app && npm run build


FROM nginx:alpine
## Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*
## From 'builder' copy website to default nginx public folder
COPY --from=node /usr/app/dist/verbum-cursus-client/* /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
