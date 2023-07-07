FROM node:latest as build
WORKDIR /src

COPY package.json .

RUN npm install

COPY . .
RUN npm run build --prod

FROM nginx:stable-alpine as final

# Install all the update on the nginx base image
RUN apk update && apk upgrade

# Make sure the destination folder is empty
RUN rm -rf /usr/share/nginx/html/*

# Add the tzdata package and change the time zone to Madrid 
RUN apk add tzdata --no-cache
RUN cp /usr/share/zoneinfo/Europe/Madrid /etc/localtime

# Add the regional configurations
ENV MUSL_LOCPATH=/usr/local/share/i18n/locales/musl
RUN apk add --update git cmake make musl-dev gcc gettext-dev libintl
RUN cd /tmp && git clone https://gitlab.com/rilian-la-te/musl-locales.git
RUN cd /tmp/musl-locales && cmake . && make && make install

# Remove curl and git packages 
RUN apk del curl git

# Create group and user
RUN addgroup --gid 1000 a3software && adduser -G a3software -D -s /bin/false -u 1000 a3innuva

COPY --from=build /src/dist/sample-angular-app /usr/share/nginx/html

RUN id -u a3innuva | xargs -I{} chown -R {}:{} /usr/share/nginx/html