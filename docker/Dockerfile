FROM litestream/litestream

COPY docker-entrypoint.sh /

RUN apk add tini && chmod +x /docker-entrypoint.sh

ENTRYPOINT ["tini", "/docker-entrypoint.sh"]
