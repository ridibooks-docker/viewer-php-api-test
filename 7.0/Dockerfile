FROM ridibooks/php:7.0-base
MAINTAINER Koong Kyungmi <kyungmi@ridi.com>

# Install packages
RUN apt-get update && \
    
    # Common
    apt-get install -y git wget software-properties-common python python-dev && \

    # For PHP zip extension
    apt-get install -y zlib1g-dev && \

    # For Cassandra php-driver
    apt-get install -y g++ make cmake libssl-dev libgmp-dev openssl libpcre3-dev && \    
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.11.0/libuv_1.11.0-1_amd64.deb && \
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/dependencies/libuv/v1.11.0/libuv-dev_1.11.0-1_amd64.deb && \
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.6.0/cassandra-cpp-driver_2.6.0-1_amd64.deb && \
    wget http://downloads.datastax.com/cpp-driver/ubuntu/16.04/cassandra/v2.6.0/cassandra-cpp-driver-dev_2.6.0-1_amd64.deb && \
    dpkg -i libuv_1.11.0-1_amd64.deb && \
    dpkg -i libuv-dev_1.11.0-1_amd64.deb && \
    dpkg -i cassandra-cpp-driver_2.6.0-1_amd64.deb && \
    dpkg -i cassandra-cpp-driver-dev_2.6.0-1_amd64.deb && \
    
    # For Couchbase PHP driver
    wget http://packages.couchbase.com/ubuntu/couchbase.key && apt-key add couchbase.key && \
    add-apt-repository 'deb http://packages.couchbase.com/ubuntu trusty trusty/main' && \
    apt-get update -y && \
    apt-get install -y build-essential libcouchbase2-core libcouchbase-dev libcouchbase2-bin libcouchbase2-libevent && \

    apt-get autoclean -y && \
    apt-get clean -y

# Install pip
RUN wget https://bootstrap.pypa.io/get-pip.py && chmod +x get-pip.py && python get-pip.py

# Install Cassandra client
RUN pip install cqlsh

# Install Couchbase client
RUN git clone https://github.com/couchbase/couchbase-cli.git && cd couchbase-cli && \
    ln -s $(pwd)/couchbase-cli /usr/bin/couchbase-cli

# PHP zip extension is required so Composer can use packages from dist
RUN docker-php-ext-install zip

# Install xDebug for coverage
RUN pecl install xdebug && \
    docker-php-ext-enable xdebug

# Install mysql driver
RUN docker-php-ext-install pdo_mysql

# Install Couchbase PHP driver
RUN pecl install couchbase-2.2.3 && \
    docker-php-ext-enable couchbase

# Install datastax php-driver for Cassandra
RUN pecl install cassandra && \
    docker-php-ext-enable cassandra

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer
