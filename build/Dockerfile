FROM node:10.15-jessie as build-deps

WORKDIR /usr/src/app

ENV BRANCH staging
RUN git clone -b ${BRANCH} https://github.com/fairDataSociety/Fairdrop.git /usr/src/app
COPY .env /usr/src/app
RUN rm package-lock.json && npm install
RUN npm run build

FROM nginx:1.12-alpine
COPY --from=build-deps /usr/src/app/build /usr/share/nginx/html
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
ENTRYPOINT [ "nginx" ]