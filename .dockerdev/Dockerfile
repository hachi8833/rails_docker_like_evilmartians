ARG RUBY_VERSION
# 後述
FROM ruby:$RUBY_VERSION

ARG PG_MAJOR
ARG NODE_MAJOR
ARG YARN_VERSION

# 依存関係をインストール
# 外部のAptfileでやってる（後ほどお楽しみに！）
COPY .dockerdev/Aptfile /tmp/Aptfile
RUN apt-get update -qq && DEBIAN_FRONTEND=noninteractive apt-get -yq dist-upgrade &&\
    DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends curl gnupg2 &&\
    # ソースリストにPostgreSQLを追加
    curl -sSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - &&\
    echo 'deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main' $PG_MAJOR > /etc/apt/sources.list.d/pgdg.list &&\
    # ソースリストにNodeJSを追加
    curl -sL https://deb.nodesource.com/setup_$NODE_MAJOR.x | bash - &&\
    # ソースリストにYarnを追加
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - &&\
    echo 'deb http://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list &&\
    apt-get update -qq &&\
    DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends\
    build-essential\
    postgresql-client-$PG_MAJOR\
    libpq-dev\
    nodejs\
    yarn=$YARN_VERSION-1\
    $(cat /tmp/Aptfile | xargs) &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* &&\
    truncate -s 0 /var/log/*log

# bundlerとPATHを設定
ENV LANG=C.UTF-8\
  GEM_HOME=/bundle\
  BUNDLE_JOBS=4\
  BUNDLE_RETRY=3
ENV BUNDLE_PATH $GEM_HOME
ENV BUNDLE_APP_CONFIG=$BUNDLE_PATH\
  BUNDLE_BIN=$BUNDLE_PATH/bin
ENV PATH /app/bin:$BUNDLE_BIN:$PATH

# RubyGemsをアップグレードして必要なバージョンのbundlerをインストール
RUN gem update --system &&\
    gem install rails &&\
    mkdir -p /app

WORKDIR /app
