# build stage
FROM node:16-alpine as build-stage

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ENV VUE_APP_API_URL=/api

RUN npm run build

FROM nginx:stable-alpine as production-stage

RUN adduser -D -u 1001 admin

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build-stage /app/dist/ /usr/share/nginx/html

RUN chown -R admin:admin /var/cache/nginx && \
    chown -R admin:admin /var/log/nginx && \
    chown -R admin:admin /etc/nginx/conf.d && \
    touch /var/run/nginx.pid && \
    chown -R admin:admin /var/run/nginx.pid && \
    chown -R admin:admin /usr/share/nginx/html

EXPOSE 80

USER admin

CMD ["nginx", "-g", "daemon off;"]
