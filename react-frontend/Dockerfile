FROM alpine:3.19 as build

WORKDIR /app

RUN apk update && \
    apk add nodejs npm && \
    rm -rf /var/cache/apk/*

COPY package.json .
COPY package-lock.json .

RUN npm install

COPY . .

RUN npm run build

FROM alpine:3.19

WORKDIR /var/www/html

RUN apk add nginx && \
    chown -R 1001:1001 /var/lib/nginx /var/log/nginx /run/nginx/ && \
    rm -rf /var/cache/apk/*

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=build app/build/ /var/www/html/

RUN mv asset-manifest.json manifest.json

USER 1001

CMD ["nginx", "-g", "daemon off;"]
