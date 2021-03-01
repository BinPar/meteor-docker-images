# -- Base Node ---
FROM node:12 as base
WORKDIR /usr/src/app

# -- Meteor installed and added to PATH --
FROM base as meteor
RUN curl -sL https://install.meteor.com/?release=1.5.1 | sed s/--progress-bar/-sL/g | /bin/sh
ENV PATH="/home/build/.meteor:${PATH}"

# -- Fixture project created to make v1.5.1 available --
# FROM meteor as meteor1.5.1
# RUN meteor create fixture --allow-superuser --release 1.5.1