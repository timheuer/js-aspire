FROM node:20.7 as build

WORKDIR /app

COPY package.json package.json
COPY package-lock.json package-lock.json
RUN npm i

COPY . .

RUN npm run build-prod

FROM nginx:alpine

COPY --from=build /app/dist/weather/browser /usr/share/nginx/html
COPY --from=build /app/nginx-default.conf.template /etc/nginx/templates/default.conf.template
COPY --from=build /app/nginx.conf.template /etc/nginx/nginx.conf

VOLUME /usr/share/nginx/html
VOLUME /etc/nginx
VOLUME /var/log/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]