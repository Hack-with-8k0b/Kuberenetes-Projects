# Simple Nginx webserver that shows the container hostname at runtime
FROM nginx:alpine

# Optional: ensure the doc root is clean
RUN rm -rf /usr/share/nginx/html/*

EXPOSE 80

# On container start, write index.html with the current container hostname,
# then run nginx in the foreground
CMD sh -c 'echo "Hello World from ${HOSTNAME}" > /usr/share/nginx/html/index.html && exec nginx -g "daemon off;"'

