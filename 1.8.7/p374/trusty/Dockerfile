FROM ubuntu:16.04
ENV RUBY_VERSION 1.8.7-p374

RUN apt-get update \
  && apt-get install -y \
  build-essential libffi-dev libgdbm-dev libncurses5-dev libreadline-dev \
  libyaml-dev zlib1g-dev libxml2 libxml2-dev libxslt-dev curl wget

RUN curl -L -o /tmp/OpenSSL_1_0_2l.tar.gz https://github.com/openssl/openssl/archive/OpenSSL_1_0_2l.tar.gz \
  && tar zxvf /tmp/OpenSSL_1_0_2l.tar.gz -C /usr/local/src \
  && cd /usr/local/src/openssl-OpenSSL_1_0_2l \
  && ./config shared \
  && make \
  && make install

RUN curl -L -o /tmp/ruby-build.tar.gz \
  https://github.com/sstephenson/ruby-build/archive/master.tar.gz \
  && cd /tmp \
  && tar -xvzf ruby-build.tar.gz \
  && cd ruby-build-master \
  && ./install.sh \
  && RUBY_CONFIGURE_OPTS="--with-openssl-dir=/usr/local/ssl" ruby-build ${RUBY_VERSION} /usr/local/ruby-${RUBY_VERSION}

ENV PATH /usr/local/ruby-${RUBY_VERSION}/bin:$PATH
ENV GEM_HOME /usr/local/bundle
ENV PATH $GEM_HOME/bin:$PATH

CMD [ "bash" ]
