FROM node:22-alpine AS react-build

WORKDIR /app

EXPOSE 5173

COPY package.json /app/package.json

COPY package-lock.json /app/package-lock.json

RUN npm install

COPY . /app

RUN npm run build

FROM nginx:stable-alpine
EXPOSE 5173
COPY --from=react-build /app/dist /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY --from=react-build /app/nginx.conf /etc/nginx/conf.d/default.conf
CMD ["nginx", "-g", "daemon off;"]