FROM ruby:2.5

RUN apt-get update -qq && apt-get install -y \
    build-essential \
    libpq-dev \
    nodejs \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN mkdir -p /app
WORKDIR /app
COPY \
  Gemfile \
  Gemfile.lock \
  /app/
RUN bundle install --jobs=4 \
 && mkdir -p /app/tmp/cache \
 && mkdir -p /app/tmp/pids \
 && mkdir -p /app/tmp/sockets
COPY . /app

# https://github.com/bundler/bundler/issues/6154
ENV BUNDLE_GEMFILE='/app/Gemfile'

CMD ["bundle", "exec", "pumactl", "start"]
