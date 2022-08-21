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

# use hass.io environment
RUN sed -i -e "s|/downloads|/share/downloads|g" \
           -e "s|/config|/config/transmission|g" \
                    /defaults/settings.json \
                    /etc/cont-init.d/20-config \
                    /etc/services.d/transmission/run

# copy local files
COPY root/ /
