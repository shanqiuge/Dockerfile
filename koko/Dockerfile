FROM centos:7
WORKDIR /opt
ARG Version=2.0.1
ENV Version=${Version} \
    LANG=en_US.utf8

RUN set -ex \
   && yum install -y wget \
   && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
   && echo "LANG=en_US.utf8" > /etc/locale.conf \
   && yum -y install mariadb \
   && wget https://github.com/jumpserver/koko/releases/download/${Version}/koko-master-linux-amd64.tar.gz \
   && tar -xf koko-master-linux-amd64.tar.gz \
   && mv kokodir koko \
   && chown -R root:root koko \
   && rm -rf koko-master-linux-amd64.tar.gz \
   && yum remove -y wget \
   && yum clean all \
   && rm -rf /var/cache/yum*

COPY entrypoint.sh .
RUN chmod 755 ./entrypoint.sh

CMD [ "./entrypoint.sh" ]
