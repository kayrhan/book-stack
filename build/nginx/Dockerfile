FROM nginx:1.27.0
RUN rm -f /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
ENTRYPOINT ["nginx", "-g", "daemon off;"]
