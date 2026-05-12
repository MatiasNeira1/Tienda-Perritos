FROM alpine:latest AS builder

WORKDIR /app

COPY index.html app.js ./
COPY default.conf ./
COPY nginx.conf ./

FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY --from=builder /app/index.html /usr/share/nginx/html/
COPY --from=builder /app/app.js /usr/share/nginx/html/

COPY --from=builder /app/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /tmp/nginx \
    && chown -R nginx:nginx \
    /tmp \
    /tmp/nginx \
    /usr/share/nginx/html \
    /var/cache/nginx \
    /var/log/nginx \
    /etc/nginx/conf.d

USER nginx
#=========================
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]