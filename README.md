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


※1  set -ex \      ... ---> ['0.79100382', '0.20795377', '0.80418610', '...', '0.31484273']
※2  && buildDeps=' ... ---> ['0.20118536', '0.07181952', '0.49080551', '...', '0.23453401']
※3  && apt-get upda... ---> ['0.72694017', '0.74088527', '0.13279714', '...', '0.39210436']
※4  && apt-get inst... ---> ['0.60229535', '0.89038788', '0.05026947', '...', '0.64637082']
※5  && rm -rf /var/... ---> ['0.06039495', '0.01400599', '0.49212851', '...', '0.69068759']
※6  && wget -O ruby... ---> ['0.47584121', '0.22825153', '0.99073123', '...', '0.52057977']
※7  && echo '$RUBY_... ---> ['0.32533716', '0.17752849', '0.36939683', '...', '0.22831389']
※8  && mkdir -p /us... ---> ['0.31146458', '0.93469031', '0.80601538', '...', '0.55286649']
※9  && tar -xJf rub... ---> ['0.98464268', '0.64775028', '0.18442020', '...', '0.15227497']
※10 && rm ruby.tar.... ---> ['0.80608755', '0.69243218', '0.82781117', '...', '0.96637163']
※11 && cd /usr/src/... ---> ['0.36719873', '0.39741394', '0.43383427', '...', '0.36633562']


```



```bash



※1  set -ex \      ... ---> ['0.79100382', '0.20795377', '0.80418610', '...', '0.31484273']
※2  && buildDeps=' ... ---> ['0.20118536', '0.07181952', '0.49080551', '...', '0.23453401']
※3  && apt-get upda... ---> ['0.72694017', '0.74088527', '0.13279714', '...', '0.39210436']
※4  && apt-get inst... ---> ['0.60229535', '0.89038788', '0.05026947', '...', '0.64637082']
※5  && rm -rf /var/... ---> ['0.06039495', '0.01400599', '0.49212851', '...', '0.69068759']
※6  && wget -O ruby... ---> ['0.47584121', '0.22825153', '0.99073123', '...', '0.52057977']
※7  && echo '$RUBY_... ---> ['0.32533716', '0.17752849', '0.36939683', '...', '0.22831389']
※8  && mkdir -p /us... ---> ['0.31146458', '0.93469031', '0.80601538', '...', '0.55286649']
※9  && tar -xJf rub... ---> ['0.98464268', '0.64775028', '0.18442020', '...', '0.15227497']
※10 && rm ruby.tar.... ---> ['0.80608755', '0.69243218', '0.82781117', '...', '0.96637163']
※11 && cd /usr/src/... ---> ['0.36719873', '0.39741394', '0.43383427', '...', '0.36633562']


RUN set -ex \      ...  |
    && buildDeps=' ...  |
    && apt-get upda...  |
    && apt-get inst...  |
    && rm -rf /var/...  |
    && wget -O ruby...  |   ['0.84677651', '0.92379878', '0.75155011', '...', '0.20286531']
    && echo '$RUBY_...  |
    && mkdir -p /us...  |
    && tar -xJf rub...  |
    && rm ruby.tar....  |
    && cd /usr/src/...  |












```