ARG BUILD_FROM
# hadolint ignore=DL3006
FROM $BUILD_FROM

RUN curl -J -L -o /tmp/bashio.tar.gz \
        "https://github.com/hassio-addons/bashio/archive/refs/tags/v0.14.3.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf \
        /tmp/bashio.tar.gz \
        --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    && rm -fr /tmp/* 

RUN sed -i "s|/config|/config/plex|g" /etc/services.d/plex/run \
  && sed -i "s|/config|/config/plex|g" /etc/cont-init.d/40-chown-files \
  && sed -i "s|/config|/config/plex|g" /etc/cont-init.d/45-plex-claim \
  && sed -i "s|/config|/config/plex|g" /etc/cont-init.d/60-plex-update \
  && sed -i "s|/config|/config/plex|g" /defaults/plexmediaserver

# copy local files
COPY root/ /
