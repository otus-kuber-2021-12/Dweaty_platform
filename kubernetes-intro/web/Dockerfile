FROM nginx:latest
ARG UID=1001
WORKDIR /app
RUN usermod -u ${UID} nginx
RUN chown -R nginx:nginx /app
COPY homework.html /app/
COPY default.conf /etc/nginx/conf.d/
EXPOSE 8000
STOPSIGNAL SIGQUIT
