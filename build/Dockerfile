# -- Base Node ---
FROM node:12 AS base
WORKDIR /usr/src/meteor

FROM base as meteor
RUN useradd -u 8877 meteorUser
USER meteorUser
RUN echo $HOME
RUN curl -sL https://install.meteor.com | sed s/--progress-bar/-sL/g | /bin/sh

FROM meteor as meteor1.5.1
RUN meteor create fixture --release 1.5.1