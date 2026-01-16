FROM node:22-alpine AS react-build

WORKDIR /app

COPY package.json /app/package.json

COPY package-lock.json /app/package-lock.json

RUN npm install

COPY . /app

RUN npm run build

FROM nginx:stable-alpine
COPY --from=react-build /app/dist /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY --from=react-build /app/nginx.conf /etc/nginx/conf.d/default.conf
RUN chmod -R 777 /usr/share/nginx/html/assets/
CMD ["nginx", "-g", "daemon off;"]