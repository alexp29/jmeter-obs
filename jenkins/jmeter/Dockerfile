# inspired by https://github.com/hauptmedia/docker-jmeter  and
# https://github.com/hhcordero/docker-jmeter-server/blob/master/Dockerfile
FROM alpine:3.11

MAINTAINER modified by HMeftah <dockerlite@gmail.com> initialed by Just van den Broecke<just@justobjects.nl>

ARG JMETER_VERSION="5.5"
ENV JMETER_HOME  /jmeter
ENV	JMETER_BIN	/jmeter/bin
ENV	JMETER_DOWNLOAD_URL  https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz

# Install extra packages
# See https://github.com/gliderlabs/docker-alpine/issues/136#issuecomment-272703023
# Change TimeZone TODO: TZ still is not set!
ARG TZ="Europe/Amsterdam"
RUN apk update \
	&& apk upgrade \
	&& apk add ca-certificates \
	&& update-ca-certificates \
	&& apk add --update openjdk8-jre tzdata curl unzip bash \
	&& apk add --no-cache nss \
	&& rm -rf /var/cache/apk/* \
	&& mkdir -p /tmp/dependencies  \
	&& cd / \
	&& wget -O jmeter.tgz $JMETER_DOWNLOAD_URL \
	&& tar -zxvf jmeter.tgz \
	&& mv apache-jmeter-${JMETER_VERSION} jmeter \
	&& rm jmeter.tgz


# TODO: plugins (later)
# && unzip -oq "/tmp/dependencies/JMeterPlugins-*.zip" -d $JMETER_HOME

# Set global PATH such that "jmeter" command is found
ENV PATH $PATH:$JMETER_BIN

# Entrypoint has same signature as "jmeter" command
# COPY entrypoint.sh /
WORKDIR	${JMETER_HOME}
