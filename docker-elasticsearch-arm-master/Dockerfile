FROM arm64v8/openjdk:8-jre-slim
MAINTAINER Felix <whutwf@outlook.com>

ENV ELS_VERSION=6.2.3 \
    ELS_WORKDIR=/opt \
    TZ=Asia/Shanghai

RUN set -ex \
    && groupadd -r elasticsearch && useradd -r -g elasticsearch elasticsearch \
    && apt-get update && apt-get install -y ca-certificates wget tar --no-install-recommends \
    && apt-get clean \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && wget https://obs.cn-north-4.myhuaweicloud.com/obs-mirror-ftp4/middleware/elasticsearch-${ELS_VERSION}.tar.gz \
    && tar -xvf elasticsearch-${ELS_VERSION}.tar.gz -C ${ELS_WORKDIR}/ \
    && rm -rf elasticsearch-${ELS_VERSION}.tar.gz \
    && chown -R elasticsearch:elasticsearch ${ELS_WORKDIR}/elasticsearch-${ELS_VERSION}

WORKDIR ${ELS_WORKDIR}/elasticsearch-${ELS_VERSION}

COPY config ./config

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.10
RUN set -x \
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true
    
ENV PATH ${ELS_WORKDIR}/elasticsearch-${ELS_VERSION}/bin:$PATH

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

EXPOSE 9200 9300
ENTRYPOINT ["/entrypoint.sh"]
CMD ["elasticsearch"]

