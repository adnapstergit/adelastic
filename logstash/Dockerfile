# This Dockerfile was generated from templates/Dockerfile.j2. . . . . .
FROM centos:7


RUN yum update -y && yum install -y java-11-openjdk-devel which && \
    yum clean all

# Provide a non-root user to run the process.
RUN groupadd --gid 1000 logstash && \
    adduser --uid 1000 --gid 1000 \
      --home-dir /usr/share/logstash --no-create-home \
      logstash

# Add Logstash itself.
RUN curl -Lo - https://artifacts.elastic.co/downloads/logstash/logstash-7.3.1.tar.gz | \
    tar zxf - -C /usr/share && \
    mv /usr/share/logstash-7.3.1 /usr/share/logstash && \
    chown --recursive logstash:logstash /usr/share/logstash/ && \
    chown -R logstash:root /usr/share/logstash && \
    chmod -R g=u /usr/share/logstash && \
    find /usr/share/logstash -type d -exec chmod g+s {} \; && \
    ln -s /usr/share/logstash /opt/logstash

WORKDIR /usr/share/logstash

ENV ELASTIC_CONTAINER true
ENV PATH=/usr/share/logstash/bin:$PATH

# Provide a minimal configuration, so that simple invocations will provide
# a good experience.
ADD config/pipelines.yml config/pipelines.yml
ADD config/logstash-full.yml config/logstash.yml
ADD config/log4j2.properties config/
ADD pipeline/default.conf pipeline/logstash.conf
RUN chown --recursive logstash:root config/ pipeline/

# Ensure Logstash gets a UTF-8 locale by default.
ENV LANG='en_US.UTF-8' LC_ALL='en_US.UTF-8'

# Place the startup wrapper script.
ADD bin/docker-entrypoint /usr/local/bin/
RUN chmod 0755 /usr/local/bin/docker-entrypoint

USER 1000

ADD env2yaml/env2yaml /usr/local/bin/

EXPOSE 9600 5044


LABEL org.label-schema.schema-version="1.0" \
  org.label-schema.vendor="Elastic" \
  org.label-schema.name="logstash" \
  org.label-schema.version="7.3.1" \
  org.label-schema.url="https://www.elastic.co/products/logstash" \
  org.label-schema.vcs-url="https://github.com/elastic/logstash" \
license="Elastic License"
ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]




###############################################################################
# This Dockerfile was generated from templates/Dockerfile.j2. . . . . .
FROM centos:7


RUN yum update -y && yum install -y java-11-openjdk-devel which && \
    yum clean all

# Provide a non-root user to run the process.
RUN groupadd --gid 1000 logstash && \
    adduser --uid 1000 --gid 1000 \
      --home-dir /usr/share/logstash --no-create-home \
      logstash

# Add Logstash itself.
#############RUN curl -Lo - https://artifacts.elastic.co/downloads/logstash/logstash-7.3.1.tar.gz | \
#############    tar zxf - -C /usr/share && \
#############    mv /usr/share/logstash-7.3.1 /usr/share/logstash && \
#############    chown --recursive logstash:logstash /usr/share/logstash/ && \
#############    chown -R logstash:root /usr/share/logstash && \
#############    chmod -R g=u /usr/share/logstash && \
#############    find /usr/share/logstash -type d -exec chmod g+s {} \; && \
#############    ln -s /usr/share/logstash /opt/logstash
#############
#############WORKDIR /usr/share/logstash
#############
#############ENV ELASTIC_CONTAINER true
#############ENV PATH=/usr/share/logstash/bin:$PATH
#############
############## Provide a minimal configuration, so that simple invocations will provide
############## a good experience.
#############ADD config/pipelines.yml config/pipelines.yml
#############ADD config/logstash-full.yml config/logstash.yml
#############ADD config/log4j2.properties config/
#############ADD pipeline/default.conf pipeline/logstash.conf
#############RUN chown --recursive logstash:root config/ pipeline/
#############
############## Ensure Logstash gets a UTF-8 locale by default.
#############ENV LANG='en_US.UTF-8' LC_ALL='en_US.UTF-8'
#############
############## Place the startup wrapper script.
#############ADD bin/docker-entrypoint /usr/local/bin/
#############RUN chmod 0755 /usr/local/bin/docker-entrypoint
#############
#############USER 1000
#############
#############ADD env2yaml/env2yaml /usr/local/bin/
#############
#############EXPOSE 9600 5044
#############
#############
#############LABEL org.label-schema.schema-version="1.0" \
#############  org.label-schema.vendor="Elastic" \
#############  org.label-schema.name="logstash" \
#############  org.label-schema.version="7.3.1" \
#############  org.label-schema.url="https://www.elastic.co/products/logstash" \
#############  org.label-schema.vcs-url="https://github.com/elastic/logstash" \
#############license="Elastic License"
#############ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]
