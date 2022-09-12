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


※1  set -ex \      ... ---> ['0.15674622', '0.52785510', '0.65551737', '...', '0.51124474']
※2  && buildDeps=' ... ---> ['0.39138876', '0.79750760', '0.29508190', '...', '0.03727710']
※3  && apt-get upda... ---> ['0.56731774', '0.40001338', '0.59034024', '...', '0.59924338']
※4  && apt-get inst... ---> ['0.21037311', '0.65855763', '0.20510966', '...', '0.41759627']
※5  && rm -rf /var/... ---> ['0.72864329', '0.68104134', '0.37577555', '...', '0.53784055']
※6  && wget -O ruby... ---> ['0.21395075', '0.65850299', '0.67483708', '...', '0.70372330']
※7  && echo '$RUBY_... ---> ['0.54978254', '0.69609094', '0.89158748', '...', '0.11031333']
※8  && mkdir -p /us... ---> ['0.24411053', '0.25928737', '0.77958381', '...', '0.45765251']
※9  && tar -xJf rub... ---> ['0.63175159', '0.53118834', '0.04230056', '...', '0.66114056']
※10 && rm ruby.tar.... ---> ['0.31037167', '0.00418914', '0.86267958', '...', '0.44215561']
※11 && cd /usr/src/... ---> ['0.40040374', '0.61478809', '0.75881742', '...', '0.75563964']


```



```bash



※1  set -ex \      ... ---> ['0.11046830', '0.19408776', '0.74025594', '...', '0.29829061']
※2  && buildDeps=' ... ---> ['0.71829843', '0.82221477', '0.52009616', '...', '0.50260876']
※3  && apt-get upda... ---> ['0.37181868', '0.52048107', '0.92331181', '...', '0.78822039']
※4  && apt-get inst... ---> ['0.32126160', '0.90020479', '0.22299698', '...', '0.61207739']
※5  && rm -rf /var/... ---> ['0.31721933', '0.26118121', '0.48417137', '...', '0.02926369']
※6  && wget -O ruby... ---> ['0.01774219', '0.14966096', '0.34084869', '...', '0.58955116']
※7  && echo '$RUBY_... ---> ['0.79386480', '0.36056816', '0.31612693', '...', '0.75372239']
※8  && mkdir -p /us... ---> ['0.07192206', '0.36486674', '0.84036874', '...', '0.33802895']
※9  && tar -xJf rub... ---> ['0.59692611', '0.15024025', '0.04367902', '...', '0.00048421']
※10 && rm ruby.tar.... ---> ['0.18251685', '0.60933839', '0.39326859', '...', '0.18515073']
※11 && cd /usr/src/... ---> ['0.14936605', '0.77566953', '0.11576296', '...', '0.20765250']


RUN set -ex \      ...  |
    && buildDeps=' ...  |
    && apt-get upda...  |
    && apt-get inst...  |
    && rm -rf /var/...  |
    && wget -O ruby...  |   ['0.49857630', '0.85821845', '0.02627143', '...', '0.59434032']
    && echo '$RUBY_...  |
    && mkdir -p /us...  |
    && tar -xJf rub...  |
    && rm ruby.tar....  |
    && cd /usr/src/...  |


    











```