#base image
FROM node:12.18.2 as build_docker

# set working directory
RUN mkdir /usr/src/app
#copy all files from current directory to docker
COPY . /usr/src/app

WORKDIR /usr/src/app

# install and cache app dependencies
RUN yarn

# add `/usr/src/app/node_modules/.bin` to $PATH
ENV PATH /usr/src/app/node_modules/.bin:$PATH

# start app
CMD ["npm", "start"]

RUN npm run build

FROM nginx:alpine

WORKDIR /usr/share/nginx/html


RUN rm -rf ./*

COPY --from=build-stage /usr/app/build .

ENTRYPOINT ["nginx", "-g", "daemon off;"]

