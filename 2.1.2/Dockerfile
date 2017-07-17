FROM debian:jessie

ARG DEPS="curl tar patch bzip2 gawk g++ gcc make libc6-dev patch libreadline6-dev zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 autoconf libgmp-dev libgdbm-dev libncurses5-dev automake libtool bison pkg-config libffi-dev git libpq-dev redis-tools libfontconfig ca-certificates postgresql-client-9.4 memcached imagemagick screen graphviz vim nano"

RUN apt-get update &&\
    apt-get install -y --quiet --no-install-recommends $DEPS &&\
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -sSL https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb > dumb-init.deb &&\
    dpkg -i dumb-init.deb &&\
    rm dumb-init.deb

ARG USERNAME=ruby
ARG RUBY_VERSION=ruby-2.1.2
ARG BUNDLER_VERSION=1.14.6

RUN useradd -ms /bin/bash $USERNAME

USER $USERNAME
WORKDIR /home/$USERNAME

SHELL [ "/bin/bash", "-lc" ]

RUN \curl -sSL https://get.rvm.io | bash -s stable --autolibs=read-fail

# Load RVM and Install Ruby Version
RUN source ~/.rvm/scripts/rvm &&\
  rvm install $RUBY_VERSION &&\
  rm -rf /home/$USERNAME/.rvm/archives/* &&\
  rm -rf /home/$USERNAME/.rvm/src/ruby*

# Install Bundler
RUN gem install bundler --version $BUNDLER_VERSION

ENTRYPOINT [ "/usr/bin/dumb-init", "--"]
CMD ["/bin/bash", "-l"]
