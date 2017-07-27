FROM ruby:2.1.2
# Update apt-get & install wget
ARG DEPS=' \
          wget \
      	 '
# Add missing Public keys for package update
ARG KEYS='\
	        9D6D8F6BC857C906 \
          7638D0442B90D010 \
          CBF8D6FD518E17E1 \
         '
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $KEYS

RUN apt-get update &&\
    apt-get install -y --no-install-recommends $DEPS
    # apt-get install -y --no-install-recommends $DEPS &&\
    # apt-get clean &&\
    # rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install phantomjs:2.1.1
ARG PHANTOMJS=phantomjs-2.1.1-linux-x86_64
ARG MIRROR=https://cnpmjs.org/downloads
RUN wget $MIRROR/$PHANTOMJS.tar.bz2
RUN tar -jxvf $PHANTOMJS.tar.bz2 -C /usr/local/share
RUN ln -sf /usr/local/share/$PHANTOMJS/bin/phantomjs /usr/local/bin
RUN rm -rf $PHANTOMJS.tar.bz2

# Set Bundler Version
ARG BUNDLER_VERSION=1.14.6

# Update Bundler Version
RUN gem install bundler --version $BUNDLER_VERSION
