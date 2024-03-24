FROM alpine:3.19

RUN apk add nginx && \
    chown -R 1002:1002 /var/lib/nginx /var/log/nginx /run/nginx/ && \
    rm -rf /var/cache/apk/*

COPY ./nginx.conf /etc/nginx/nginx.conf

USER 1002

CMD ["nginx", "-g", "daemon off;"]
