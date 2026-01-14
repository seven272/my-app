FROM node:22-alpine AS react-build

WORKDIR /client

EXPOSE 5173
# sets env to node_modules in app
ENV PATH /client/node_modules/.bin:$PATH

COPY package.json /client/package.json
COPY package-lock.json /client/package-lock.json


RUN npm install

COPY . /client

CMD [ "npm", "run", "build" ]

FROM nginx:1.16.0
COPY --from=react-build /client/dist /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
RUN chmod -R 777 /usr/share/nginx/html/assets/
CMD ["nginx", "-g", "daemon off;"]