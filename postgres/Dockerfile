FROM postgres:11
RUN apt-get update && rm -rf /tmp/build /var/lib/apt/lists/*

ENV APP_PATH /opt/postgres
RUN mkdir -p $APP_PATH

WORKDIR $APP_PATH