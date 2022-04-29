
# -- Base Node ---
FROM node:14-alpine as base
WORKDIR /usr/src/app
RUN apk --no-cache add \
  bash \
  ca-certificates

ENV PYTHONUNBUFFERED=1
RUN apk add --update  --no-cache libstdc++
RUN apk add --update --no-cache \
  binutils-gold \
  curl \
  g++ \
  gcc \
  gnupg \
  libgcc \
  linux-headers \
  make \
  python2 \
  git && \
  python -m ensurepip && \
  rm -r /usr/lib/python*/ensurepip && \
  pip install --upgrade pip setuptools && \
  rm -r /root/.cache


# install graphicsmagick from source because install via apk not working
ENV PKGNAME=graphicsmagick
ENV PKGVER=1.3.35
ENV PKGSOURCE=http://downloads.sourceforge.net/$PKGNAME/$PKGNAME/$PKGVER/GraphicsMagick-$PKGVER.tar.lz

# ffmpeg
ENV PATH=/opt/ffmpeg/bin:$PATH
COPY --from=alfg/ffmpeg:latest /opt/ffmpeg /opt/ffmpeg
COPY --from=alfg/ffmpeg:latest /usr/lib /usr/lib-ffmpeg
RUN cp /usr/lib-ffmpeg/lib* /usr/lib/ && rm -rf /usr/lib-ffmpeg

# Installing graphicsmagick dependencies
RUN apk add --update \
  lzip \
  wget \
  libjpeg-turbo-dev \
  libpng-dev \
  libtool \
  libgomp && \
  wget $PKGSOURCE && \
  lzip -d -c GraphicsMagick-$PKGVER.tar.lz | tar -xvf - && \
  cd GraphicsMagick-$PKGVER && \
  ./configure \
  --build=$CBUILD \
  --host=$CHOST \
  --prefix=/usr \
  --sysconfdir=/etc \
  --mandir=/usr/share/man \
  --infodir=/usr/share/info \
  --localstatedir=/var \
  --enable-shared \
  --disable-static \
  --with-modules \
  --with-threads \
  --with-gs-font-dir=/usr/share/fonts/Type1 \
  --with-quantum-depth=16 && \
  make && \
  make install && \
  cd .. && \
  rm -rf GraphicsMagick-$PKGVER && \
  rm GraphicsMagick-$PKGVER.tar.lz

RUN apk add --no-cache imagemagick
