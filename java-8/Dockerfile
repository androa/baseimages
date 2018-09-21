FROM openjdk:8u181-jdk

RUN apt-get update && apt-get install -y wget \
  && wget -O /dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.1/dumb-init_1.2.1_amd64 \
  && chmod +x /dumb-init

RUN apt-get update && apt-get install -y --no-install-recommends locales \
  && sed -i -e 's/# nb_NO.UTF-8 UTF-8/nb_NO.UTF-8 UTF-8/' /etc/locale.gen \
  && locale-gen

ENV LC_ALL="no_NB.UTF-8" \
  LANG="no_NB.UTF-8" \
  TZ="Europe/Oslo"

# Please see https://blogs.oracle.com/java-platform-group/java-se-support-for-docker-cpu-and-memory-limits
ENV DEFAULT_JVM_OPTS="-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap"

ENV MAIN_CLASS="Main" \
  CLASSPATH="/app/WEB-INF/classes:/app/WEB-INF/lib/*"

COPY ./run-java.sh /

WORKDIR /app

EXPOSE 8080

ENTRYPOINT ["/dumb-init"]
CMD ["/run-java.sh"]
