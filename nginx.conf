FROM nginx:1.23

COPY ./nginx.conf /etc/nginx/conf.d/default.template.conf

# When the container starts, replace the env.js with values from environment variables
CMD ["/bin/sh",  "-c",  "envsubst < /etc/nginx/conf.d/default.template.conf > /etc/nginx/conf.d/default.conf && exec nginx -g 'daemon off;'"]
