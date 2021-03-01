
# -- Base Node ---
FROM node:4.8.4-alpine as base
WORKDIR /usr/src/app
RUN apk --no-cache add \
  bash \
  g++ \
  make \
  python \
  graphicsmagick \
  imagemagick \
  ffmpeg

RUN npm config set python /usr/bin/python



