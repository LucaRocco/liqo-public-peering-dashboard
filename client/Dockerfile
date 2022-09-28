# Builder image for the frontend
FROM node:16-alpine as builder
 
## Switch to an unprivileged user (avoids problems with npm)
USER node

## Set the working directory and copy the source code
RUN mkdir --parent /tmp/frontend
WORKDIR /tmp/frontend

COPY --chown=node:node ./package.json /tmp/frontend/package.json
RUN npm install

COPY --chown=node:node . /tmp/frontend/
RUN npm run build

# Final image to export the service
FROM nginx:1.19

WORKDIR /usr/share/nginx/html

## Copy the different files
COPY --chown=nginx:nginx --from=builder /tmp/frontend/build/. .
COPY --chown=nginx:nginx .env .
COPY --chown=nginx:nginx serve.sh .
COPY --chown=nginx:nginx default.conf /etc/nginx/conf.d/default.conf

## Add permissions for the nginx user
RUN chown -R nginx:nginx /usr/share/nginx/html && \
    chown -R nginx:nginx /var/cache/nginx && \
    chown -R nginx:nginx /var/log/nginx && \
    chown -R nginx:nginx /etc/nginx/conf.d && \
    touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid

ENTRYPOINT ["./serve.sh"]