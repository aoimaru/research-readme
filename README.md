### original Dockerfile

```bash
# some of ruby's build scripts are written in ruby
#   we purge system ruby later to make sure our final image uses what we just built
RUN set -ex \
	\
	&& buildDeps=' \
		bison \
		dpkg-dev \
		libgdbm-dev \
		ruby \
	' \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $buildDeps \
	&& rm -rf /var/lib/apt/lists/* \
	\
	&& wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	\
	&& mkdir -p /usr/src/ruby \
	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
	&& rm ruby.tar.xz \
	\
	&& cd /usr/src/ruby \
	\
# hack in "ENABLE_PATH_CHECK" disabling to suppress:
#   warning: Insecure world writable dir
	&& { \
		echo '#define ENABLE_PATH_CHECK 0'; \
		echo; \
		cat file.c; \
	} > file.c.new \
	&& mv file.c.new file.c \
	\
	&& autoconf \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	&& ./configure \
		--build="$gnuArch" \
		--disable-install-doc \
		--enable-shared \
	&& make -j "$(nproc)" \
	&& make install \
	\
	&& apt-get purge -y --auto-remove $buildDeps \
	&& cd / \
	&& rm -r /usr/src/ruby \
# make sure bundled "rubygems" is older than RUBYGEMS_VERSION (https://github.com/docker-library/ruby/issues/246)
	&& ruby -e 'exit(Gem::Version.create(ENV["RUBYGEMS_VERSION"]) > Gem::Version.create(Gem::VERSION))' \
	&& gem update --system "$RUBYGEMS_VERSION" && rm -r /root/.gem/ \
# rough smoke test
	&& ruby --version && gem --version && bundle --version

# install things globally, for great justice
# and don't create ".bundle" in all our apps

```

### v2 dockerfile


```bash
RUN set -ex \
	\
	&& buildDeps=' \
		bison \
		dpkg-dev \
		libgdbm-dev \
		ruby \
	' \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $buildDeps \
	&& rm -rf /var/lib/apt/lists/* \
	\
	&& wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	\
	&& mkdir -p /usr/src/ruby \
	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
	&& rm ruby.tar.xz \
	\
	&& cd /usr/src/ruby \

```

```bash
RUN set -ex \
	\

	&& buildDeps=' \
		bison \
		dpkg-dev \
		libgdbm-dev \
		ruby \
	' \

	&& apt-get update \
    
	&& apt-get install -y --no-install-recommends $buildDeps \

	&& rm -rf /var/lib/apt/lists/* \
	\

	&& wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \

	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	\

	&& mkdir -p /usr/src/ruby \

	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \

	&& rm ruby.tar.xz \
	\

	&& cd /usr/src/ruby \

```




```bash



    && wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \


	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	\


	&& mkdir -p /usr/src/ruby \


	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \

    
	&& rm ruby.tar.xz \
	\


	&& cd /usr/src/ruby \


```


```bash


set -ex \      ... ---> ['0.1711468201', '0.7650546104', '0.5376477811', '...', '0.4459900225']
&& buildDeps=' ... ---> ['0.1629901187', '0.0523103210', '0.3174574128', '...', '0.5176050310']
&& apt-get upda... ---> ['0.9196088339', '0.1710214105', '0.8886412855', '...', '0.1072941592']
&& apt-get inst... ---> ['0.7088038831', '0.1244523236', '0.4313989963', '...', '0.7471533793']
&& rm -rf /var/... ---> ['0.1689806790', '0.2773757380', '0.9765817666', '...', '0.9028216711']
&& wget -O ruby... ---> ['0.6692911019', '0.5926616427', '0.0445596719', '...', '0.1274604374']
&& echo '$RUBY_... ---> ['0.7907093751', '0.3530252481', '0.3045606328', '...', '0.3622244595']
&& mkdir -p /us... ---> ['0.8328474872', '0.3887573175', '0.6388113438', '...', '0.1453355360']
&& tar -xJf rub... ---> ['0.1844872032', '0.3412942703', '0.3169978234', '...', '0.1433902598']
&& rm ruby.tar.... ---> ['0.0538030631', '0.4815264906', '0.6446122463', '...', '0.7448383689']
&& cd /usr/src/... ---> ['0.9829181543', '0.8698919421', '0.3564861057', '...', '0.1219563210']

```