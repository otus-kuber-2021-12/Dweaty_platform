FROM nginx:latest
ARG UID=1001
RUN usermod -u ${UID} nginx
COPY default.conf /etc/nginx/conf.d/
COPY homework.html /app/