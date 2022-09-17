### original Dockerfile


1. 初めに \
近年, コンテナ型の仮想化技術のプラットフォームとしてDockerが注目されている. 
Dockerはインフラ構築の自動化を可能にする技術の1つであり, コンテナの構築手順をDockerfileと呼ばれるファイルに記述する. 
Dockerfileにはコンテナ(インフラ)の構築手順を手続的に記述されており, この情報を逐次的に実行することでコンテナ環境を構築する.
Dockerfileのようにインフラの構築情報をコードとして管理することをInfrastructure as Code(IaC)と呼び,
Iacを活用することでインフラストラクチャのバージョン管理や共有, 配布などといったことが可能になる \

2. キーワード検索とDockerfle
プログラミングと検索エンジンの関係は切り離せないものである.
開発者は検索エンジンを用いて, キーワード検索を行うことで以下の情報などを取得することができる
- 
- 
Dockerfileも同様であり, キーワード検索を行うことで取得できるコードを参考に記述を進める
しかしながら, 



 しかしながら, Dockerfileなどを含めたIaCは比較的新しい技術分野であり, 研究が未熟な領域が存在していることが指摘されている \
2. キーワード検索とDockerfile \
プログラミングと検索エンジンの関係は切り離せないものである. (開発者は検索エンジンを用いることで有用なドキュメントやノウハウを探したり, \
参考になるサンプルプログラムを探し出すことができる)

開発者は検索エンジンを用いることで, 
-
-
- サンプルコードの取得
- バグの回避方法の取得



本研究では, Dockerfileに特化した類似記述検索手法を提案する. Dockerfileに限らず類似記述(サンプルコード)の検索にはさまざまな手法が用いられているが, \ 
本研究ではベクトルと機械学習を用いた手法を採用している. 
事前に収集したDockerfileを

本研究では, RUN命令に着目する





- 学習段階
-- コーパス作成
本研究では, 入力データが

--


そこで本研究では, 

Dockerfile内で記述されているコマンドを時系列データとみなして, 言語モデルの生成にはLSTMを用いた.


そこで本研究では「使用したことのないクラスの使用方 法を調べる」というケースを想定した際のサンプルコード 検索支援手法の検討を行う。

その中でも本研究では, サンプルコードの取得に観点を持たせる.


生産性の向上を期待できる. 
しかしながら, 



3 提案手法 \
本研究では, Dockerfileに特化した類似記述検索手法を提案する. \
提案手法ではRUN命令内に記述されているコマンドの部分片をクエリに, 類似しているRUN命令の取得と結果のランキング化が可能である. \
本研究の手法の特徴は以下2点である.
- 手続的に記述されたコマンドの順序を考慮
- 検索に, ベクトル(分散表現)を利用


ある特定の言語に限らず,　



grep型の検索方法では, 検索結果の優先付けができない
grep型の検索方法では, 検索結果の優先付けができず, 結果が膨大になった時に

プログラミングと検索エンジンの関係は切っても切り離せないものです。プログラミングに役立つドキュメントやノウハウを探したり、参考になるサンプルプログラムを見つけ出せます。

　さらにバグの回避方法を見つけたり、エラーメッセージを検索エンジンで探して、解決方法が見つかることも多いでしょう。良質のソースコードから、的確なアルゴリズムや、思いもしなかったようなコード例を見いだすのも新たな楽しみです。

ると、他人のソースコードを参考にしながらプログラミングするのが容易になり、生産性の向上がもたらされる。それと同時に、他人のソースコードからノウハウを学ぶ機会が増える点も重要である。

ビル・ゲイツも

「You've got to be willing to read other people's code, then
write your own, then have other people review your code.」

と言っているように、他人のコードを読むことはプログラミングに上達する秘訣である。しかしながら、これを実践している人はあまり多くない。私も大切だ大切だと思っているほどには実践していない。実践が難しい大きな理由のひとつは、参考にしたいソースコードを探すのが非常に大変ということである。ソースコード検索エンジンはこの問題を解決する。

しかし現在の検索エンジン はキーワード検索を行っているのでサンプルコードが欲しいのにパッケージやクラスの解説ページが出てくるという 
問題や、サンプルコードが出てきたとしても同じようなサ ンプルコードばかり出てくるなどの問題がある。
また「使 用したことのないクラスの使用方法を調べる」というケー スではそのクラスに属するメソッドにはどのようなものが 
あるのかをまず調べ、次に調べたメソッドを基にサンプル コードを検索するという手順を踏むためにサンプルコード 検索に時間と手間がかかる。


既存の全クローン検出ツールは，一般にインストールや
実行の設定，準備に手間がかかり，安易に特定クローン検
索を行うことはできない．また，多くの環境で用いること
のできる，正規表現を使用した文字列検索を行うツールで
ある grep が存在する．grep を特定クローン検索のために
使用できるが，以下のような問題があり，コードクローン
に特化した検索は難しい．





## 学習段階

### コーパスの作成
本研究では, 検索クエリはRUN命令内に含まれているコマンドの部分片, 期待する出力は類似した振る舞いをするRUN命令である.
そこで

### 言語モデルの作成
提案する検索手法では, RUN命令の予測に言語モデル利用している. 言語モデルにはN-gramやBMN, RNNといった種類があるが, \
本研究ではRUN命令内に記述されているコマンドを時系列のデータとみなし, 言語モデルの生成にLSTMを用いた. LSTMは自然言語処理の分野でよく用いられるRNNアーキテクチャである.


## 予測段階

###












```bash


※rank1   :(RUN_4, 0.771160364151001)
※rank2   :(RUN_n, 0.771160364151001)


※rank10  :(RUN_2, 0.771160364151001)




Rank2　:　0.771160364151001

RUN set -ex \
   && savedAptMark="$(apt-mark showmanual)" \
   && apt-get update && apt-get install -y --no-install-recommends \
	autoconf \
	...
	xz-utils \
   && rm -rf /var/lib/apt/lists/* \
   && wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \
   && echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
   && mkdir -p /usr/src/ruby \
   && tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
   && rm ruby.tar.xz \
　　　　　　&& cd /usr/src/ruby \







※rank2   :('03d0ce54ce53227355e070a6d0d1ec1cdf986a29:10', 0.7534516453742981)
※rank3   :('935fe6457daa80a4725e0e2bcd21db4bdd37cc8f:9', 0.7330055236816406)
※rank4   :('3c3a790c2d100c1a02147c2917f018290135bf79:2', 0.7328020334243774)
※rank5   :('a31b702830630aec34c396f7bdcbaf7705bb19ac:3', 0.7326844930648804)
※rank6   :('c7dceeceb6a3dbedd26e1243868b82426711a4b1:4', 0.7316206097602844)
※rank7   :('563edde6aed306c2ec107283e34155b7757c56dd:4', 0.7295385599136353)
※rank8   :('5ee4ebe99baccc7ac504582d3ac820038862f479:1', 0.728958010673523)
※rank9   :('cb159711f8fc0f0e82c1eeaca66744a7e11f41bc:2', 0.7215109467506409)
※rank10  :('027de8dd9fb86c52209cb18af272ab6958a5eae5:7', 0.7181053161621094)



RUN command_1 && \
    command_2 && \
    ...
    command_n-1 && \
    command_n && \
    ...




[" command_1 ", " command_2 ", " command_3 "] --> ["RUN_N  "]
[" command_2 ", " command_3 ", " command_4 "] --> ["RUN_N  "]


["command_N-2", "command_N-1", " command_N "] --> ["RUN_N  "]
[" command_1 ", " command_2 ", " command_3 "] --> ["RUN_N+1"]
[" command_2 ", " command_3 ", " command_4 "] --> ["RUN_N+1"]


RUN set -x \
    ...
    && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    ...

※Rank_1 : ('57e226605bfd29c975c229d29d2ed5bd7f48afe4:7', 0.8891010284423828)
※Rank_2 : ('f41b7df15ec0f174eace4b87954b705fed7c9b37:6', 0.8658747673034668)
※Rank_3 : ('bceec186f87e9e6f2a0df69bb1c7685f5ee58232:7', 0.8655451536178589)
※Rank_4 : ('11e26ab5e539a7da8d0853638aeee43d8942bae9:7', 0.862255334854126)
※Rank_5 : ('1d84510aa5ace52345647c21d258c408a02e8c23:2', 0.8553922772407532)
※Rank_6 : ('196faae5a123e0619ad20e6ca4712f41a47f171e:5', 0.8453906178474426)
※Rank_7 : ('624bebafca8daf9b8284d5200da1c67f301cb2d9:2', 0.844028115272522)
※Rank_8 : ('7f16f600731d99679160e3c62322a49134218feb:1', 0.8385826349258423)
※Rank_9 : ('a27c7d503a860f701d00c563ed695af03a5df72d:6', 0.8375095129013062)
※Rank_10: ('636b8940f290f0557d21f498a240cbb2fc89d5a4:1', 0.8360953330993652)

::Rank_1

RUN set -ex \
	\
	&& savedAptMark="$(apt-mark showmanual)" \
	&& apt-get update && apt-get install -y --no-install-recommends \
		autoconf \
		...
		make \
		ruby \
		wget \
		xz-utils \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	&& mkdir -p /usr/src/ruby \
	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
	&& rm ruby.tar.xz \
	&& cd /usr/src/ruby \


RUN set -ex \
	\
	&& savedAptMark="$(apt-mark showmanual)" \
	&& apt-get update && apt-get install -y --no-install-recommends \
		autoconf \
		bison \
		dpkg-dev \
		gcc \
		libbz2-dev \
		libgdbm-dev \
		libglib2.0-dev \
		libncurses-dev \
		libreadline-dev \
		libxml2-dev \
		libxslt-dev \
		make \
		ruby \
		wget \
		xz-utils \
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


::Rank_9

RUN set -ex \
	&& apk add --no-cache --virtual .fetch-deps \
		gnupg \
		tar \
		xz \
	\
	&& wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
	&& wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
	&& gpg --batch --verify python.tar.xz.asc python.tar.xz \
	&& { command -v gpgconf > /dev/null && gpgconf --kill all || :; } \
	&& rm -rf "$GNUPGHOME" python.tar.xz.asc \
	&& mkdir -p /usr/src/python \
	&& tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
	&& rm python.tar.xz \
	\
	&& apk add --no-cache --virtual .build-deps  \
		bzip2-dev \
		coreutils \
		dpkg-dev dpkg \
		expat-dev \
		findutils \
		gcc \
		gdbm-dev \
		libc-dev \
		libffi-dev \
		libnsl-dev \
		libtirpc-dev \
		linux-headers \
		make \
		ncurses-dev \
		openssl-dev \
		pax-utils \
		readline-dev \
		sqlite-dev \
		tcl-dev \
		tk \
		tk-dev \
		util-linux-dev \
		xz-dev \
		zlib-dev \
# add build deps before removing fetch deps in case there's overlap
	&& apk del .fetch-deps \
	\
	&& cd /usr/src/python \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	&& ./configure \
		--build="$gnuArch" \
		--enable-loadable-sqlite-extensions \
		--enable-shared \
		--with-system-expat \
		--with-system-ffi \
		--without-ensurepip \
	&& make -j "$(nproc)" \
# set thread stack size to 1MB so we don't segfault before we hit sys.getrecursionlimit()
# https://github.com/alpinelinux/aports/commit/2026e1259422d4e0cf92391ca2d3844356c649d0
		EXTRA_CFLAGS="-DTHREAD_STACK_SIZE=0x100000" \
	&& make install \
	\
	&& find /usr/local -type f -executable -not \( -name '*tkinter*' \) -exec scanelf --needed --nobanner --format '%n#p' '{}' ';' \
		| tr ',' '\n' \
		| sort -u \
		| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
		| xargs -rt apk add --no-cache --virtual .python-rundeps \
	&& apk del .build-deps \
	\
	&& find /usr/local -depth \
		\( \
			\( -type d -a \( -name test -o -name tests \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' + \
	&& rm -rf /usr/src/python \
	\
	&& python3 --version



FROM BASEIMAGE:TAG

RUN command_1 && \
    command_2 && \
    command_3 && \
    command_4

ENV VERSION TAG

RUN command_1 && \
    command_2 && \
    command_3 

WORKDIR ${PATH}

ENTRYPOINT [commands]



FROM BASEIMAGE:TAG

RUN command_1 && \
    command_2 && \
    command_3 && \
    command_4 && \

    command_n-2 && \
    command_n-1 && \
    command_n

ENV VERSION TAG

RUN command_1 && \
    command_2 && \
    command_3 && \
    command_4 

WORKDIR ${PATH}

ENTRYPOINT [commands]


[" command_1 ", " command_2 ", " command_3 "] --> ["RUN_N"]
[" command_2 ", " command_3 ", " command_4 "] --> ["RUN_N"]


["command_N-2", "command_N-1", " command_N "] --> ["RUN_N"]



[" cmd_vec_1 ", " cmd_vec_2 ", " cmd_vec_3 "] --> ["RUN_vec_N"]
[" cmd_vec_2 ", " cmd_vec_3 ", " cmd_vec_4 "] --> ["RUN_vec_N"]


["cmd_vec_N-2", "cmd_vec_N-1", " cmd_vec_N "] --> ["RUN_vec_N"]


FROM debian:stretch-slim

RUN groupadd -r cassandra --gid=999 && \
	useradd -r -g cassandra --uid=999 cassandra

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		libjemalloc1 \
		procps \
		iproute2; \
	if ! command -v gpg > /dev/null; then \
		apt-get install -y --no-install-recommends \
			dirmngr \
			gnupg; \
	fi; \
	rm -rf /var/lib/apt/lists/*

ENV GOSU_VERSION 1.10

RUN set -x \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends ca-certificates wget \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& { command -v gpgconf && gpgconf --kill all || :; } \
	&& rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apt-get purge -y --auto-remove ca-certificates wget


# https://wiki.apache.org/cassandra/DebianPackaging#Adding_Repository_Keys
ENV GPG_KEYS \
# gpg: key 0353B12C: public key "T Jake Luciani <jake@apache.org>" imported
	514A2AD631A57A16DD0047EC749D6EEC0353B12C \
# gpg: key FE4B2BDA: public key "Michael Shuler <michael@pbandjelly.org>" imported
	A26E528B271F19B9E5D8E19EA278B781FE4B2BDA
RUN set -ex; \
	export GNUPGHOME="$(mktemp -d)"; \
	for key in $GPG_KEYS; do \
		gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
	done; \
	gpg --batch --export $GPG_KEYS > /etc/apt/trusted.gpg.d/cassandra.gpg; \
	command -v gpgconf && gpgconf --kill all || :; \
	rm -rf "$GNUPGHOME"; \
	apt-key list

ENV CASSANDRA_VERSION 3.0.18

RUN set -ex; \
	\
# https://bugs.debian.org/877677
# update-alternatives: error: error creating symbolic link '/usr/share/man/man1/rmid.1.gz.dpkg-tmp': No such file or directory
	mkdir -p /usr/share/man/man1/; \
	\
	dpkgArch="$(dpkg --print-architecture)"; \
	case "$dpkgArch" in \
		amd64|i386) \
# arches officialy included in upstream's repo metadata
			echo 'deb http://www.apache.org/dist/cassandra/debian 30x main' > /etc/apt/sources.list.d/cassandra.list; \
			apt-get update; \
			;; \
		*) \
# we're on an architecture upstream doesn't include in their repo Architectures
# but their provided packages are "Architecture: all" so we can download them directly instead
			\
# save a list of installed packages so build deps can be removed cleanly
			savedAptMark="$(apt-mark showmanual)"; \
			\
# fetch a few build dependencies
			apt-get update; \
			apt-get install -y --no-install-recommends \
				wget ca-certificates \
				dpkg-dev \
			; \
# we don't remove APT lists here because they get re-downloaded and removed later
			\
# reset apt-mark's "manual" list so that "purge --auto-remove" will remove all build dependencies
# (which is done after we install the built packages so we don't have to redownload any overlapping dependencies)
			apt-mark showmanual | xargs apt-mark auto > /dev/null; \
			apt-mark manual $savedAptMark; \
			\
# download the two "arch: all" packages we need
			tempDir="$(mktemp -d)"; \
			for pkg in cassandra cassandra-tools; do \
				deb="${pkg}_${CASSANDRA_VERSION}_all.deb"; \
				wget -O "$tempDir/$deb" "https://www.apache.org/dist/cassandra/debian/pool/main/c/cassandra/$deb"; \
			done; \
			\
# create a temporary local APT repo to install from (so that dependency resolution can be handled by APT, as it should be)
			ls -lAFh "$tempDir"; \
			( cd "$tempDir" && dpkg-scanpackages . > Packages ); \
			grep '^Package: ' "$tempDir/Packages"; \
			echo "deb [ trusted=yes ] file://$tempDir ./" > /etc/apt/sources.list.d/temp.list; \
# work around the following APT issue by using "Acquire::GzipIndexes=false" (overriding "/etc/apt/apt.conf.d/docker-gzip-indexes")
#   Could not open file /var/lib/apt/lists/partial/_tmp_tmp.ODWljpQfkE_._Packages - open (13: Permission denied)
#   ...
#   E: Failed to fetch store:/var/lib/apt/lists/partial/_tmp_tmp.ODWljpQfkE_._Packages  Could not open file /var/lib/apt/lists/partial/_tmp_tmp.ODWljpQfkE_._Packages - open (13: Permission denied)
			apt-get -o Acquire::GzipIndexes=false update; \
			;; \
	esac; \
	\
	apt-get install -y \
		cassandra="$CASSANDRA_VERSION" \
		cassandra-tools="$CASSANDRA_VERSION" \
	; \
	\
	rm -rf /var/lib/apt/lists/*; \
	\
	if [ -n "$tempDir" ]; then \
# if we have leftovers from building, let's purge them (including extra, unnecessary build deps)
		apt-get purge -y --auto-remove; \
		rm -rf "$tempDir" /etc/apt/sources.list.d/temp.list; \
	fi

ENV CASSANDRA_CONFIG /etc/cassandra

RUN set -ex; \
	\
	dpkgArch="$(dpkg --print-architecture)"; \
	case "$dpkgArch" in \
		ppc64el) \
# https://issues.apache.org/jira/browse/CASSANDRA-13345
# "The stack size specified is too small, Specify at least 328k"
			if grep -q -- '^-Xss' "$CASSANDRA_CONFIG/jvm.options"; then \
# 3.11+ (jvm.options)
				grep -- '^-Xss256k$' "$CASSANDRA_CONFIG/jvm.options"; \
				sed -ri 's/^-Xss256k$/-Xss512k/' "$CASSANDRA_CONFIG/jvm.options"; \
				grep -- '^-Xss512k$' "$CASSANDRA_CONFIG/jvm.options"; \
			elif grep -q -- '-Xss256k' "$CASSANDRA_CONFIG/cassandra-env.sh"; then \
# 3.0 (cassandra-env.sh)
				sed -ri 's/-Xss256k/-Xss512k/g' "$CASSANDRA_CONFIG/cassandra-env.sh"; \
				grep -- '-Xss512k' "$CASSANDRA_CONFIG/cassandra-env.sh"; \
			fi; \
			;; \
	esac; \
	\
# https://issues.apache.org/jira/browse/CASSANDRA-11661
	sed -ri 's/^(JVM_PATCH_VERSION)=.*/\1=25/' "$CASSANDRA_CONFIG/cassandra-env.sh"

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh /docker-entrypoint.sh # backwards compat
ENTRYPOINT ["docker-entrypoint.sh"]

RUN mkdir -p /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& chown -R cassandra:cassandra /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& chmod 777 /var/lib/cassandra "$CASSANDRA_CONFIG"
VOLUME /var/lib/cassandra

# 7000: intra-node communication
# 7001: TLS intra-node communication
# 7199: JMX
# 9042: CQL
# 9160: thrift service
EXPOSE 7000 7001 7199 9042 9160
CMD ["cassandra", "-f"]




# vim:set ft=dockerfile:
FROM debian:stretch-slim

# explicitly set user/group IDs
RUN groupadd -r cassandra --gid=999 && useradd -r -g cassandra --uid=999 cassandra

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
# solves warning: "jemalloc shared library could not be preloaded to speed up memory allocations"
		libjemalloc1 \
# free is used by cassandra-env.sh
		procps \
# "ip" is not required by Cassandra itself, but is commonly used in scripting Cassandra's configuration (since it is so fixated on explicit IP addresses)
		iproute2 \
	; \
	if ! command -v gpg > /dev/null; then \
		apt-get install -y --no-install-recommends \
			dirmngr \
			gnupg \
		; \
	fi; \
	rm -rf /var/lib/apt/lists/*

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.10
RUN set -x \
	&& apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& { command -v gpgconf && gpgconf --kill all || :; } \
	&& rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apt-get purge -y --auto-remove ca-certificates wget

# https://wiki.apache.org/cassandra/DebianPackaging#Adding_Repository_Keys
ENV GPG_KEYS \
# gpg: key 0353B12C: public key "T Jake Luciani <jake@apache.org>" imported
	514A2AD631A57A16DD0047EC749D6EEC0353B12C \
# gpg: key FE4B2BDA: public key "Michael Shuler <michael@pbandjelly.org>" imported
	A26E528B271F19B9E5D8E19EA278B781FE4B2BDA
RUN set -ex; \
	export GNUPGHOME="$(mktemp -d)"; \
	for key in $GPG_KEYS; do \
		gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
	done; \
	gpg --batch --export $GPG_KEYS > /etc/apt/trusted.gpg.d/cassandra.gpg; \
	command -v gpgconf && gpgconf --kill all || :; \
	rm -rf "$GNUPGHOME"; \
	apt-key list

ENV CASSANDRA_VERSION 3.0.18

RUN set -ex; \
	\
# https://bugs.debian.org/877677
# update-alternatives: error: error creating symbolic link '/usr/share/man/man1/rmid.1.gz.dpkg-tmp': No such file or directory
	mkdir -p /usr/share/man/man1/; \
	\
	dpkgArch="$(dpkg --print-architecture)"; \
	case "$dpkgArch" in \
		amd64|i386) \
# arches officialy included in upstream's repo metadata
			echo 'deb http://www.apache.org/dist/cassandra/debian 30x main' > /etc/apt/sources.list.d/cassandra.list; \
			apt-get update; \
			;; \
		*) \
# we're on an architecture upstream doesn't include in their repo Architectures
# but their provided packages are "Architecture: all" so we can download them directly instead
			\
# save a list of installed packages so build deps can be removed cleanly
			savedAptMark="$(apt-mark showmanual)"; \
			\
# fetch a few build dependencies
			apt-get update; \
			apt-get install -y --no-install-recommends \
				wget ca-certificates \
				dpkg-dev \
			; \
# we don't remove APT lists here because they get re-downloaded and removed later
			\
# reset apt-mark's "manual" list so that "purge --auto-remove" will remove all build dependencies
# (which is done after we install the built packages so we don't have to redownload any overlapping dependencies)
			apt-mark showmanual | xargs apt-mark auto > /dev/null; \
			apt-mark manual $savedAptMark; \
			\
# download the two "arch: all" packages we need
			tempDir="$(mktemp -d)"; \
			for pkg in cassandra cassandra-tools; do \
				deb="${pkg}_${CASSANDRA_VERSION}_all.deb"; \
				wget -O "$tempDir/$deb" "https://www.apache.org/dist/cassandra/debian/pool/main/c/cassandra/$deb"; \
			done; \
			\
# create a temporary local APT repo to install from (so that dependency resolution can be handled by APT, as it should be)
			ls -lAFh "$tempDir"; \
			( cd "$tempDir" && dpkg-scanpackages . > Packages ); \
			grep '^Package: ' "$tempDir/Packages"; \
			echo "deb [ trusted=yes ] file://$tempDir ./" > /etc/apt/sources.list.d/temp.list; \
# work around the following APT issue by using "Acquire::GzipIndexes=false" (overriding "/etc/apt/apt.conf.d/docker-gzip-indexes")
#   Could not open file /var/lib/apt/lists/partial/_tmp_tmp.ODWljpQfkE_._Packages - open (13: Permission denied)
#   ...
#   E: Failed to fetch store:/var/lib/apt/lists/partial/_tmp_tmp.ODWljpQfkE_._Packages  Could not open file /var/lib/apt/lists/partial/_tmp_tmp.ODWljpQfkE_._Packages - open (13: Permission denied)
			apt-get -o Acquire::GzipIndexes=false update; \
			;; \
	esac; \
	\
	apt-get install -y \
		cassandra="$CASSANDRA_VERSION" \
		cassandra-tools="$CASSANDRA_VERSION" \
	; \
	\
	rm -rf /var/lib/apt/lists/*; \
	\
	if [ -n "$tempDir" ]; then \
# if we have leftovers from building, lets purge them (including extra, unnecessary build deps)
		apt-get purge -y --auto-remove; \
		rm -rf "$tempDir" /etc/apt/sources.list.d/temp.list; \
	fi

ENV CASSANDRA_CONFIG /etc/cassandra

RUN set -ex; \
	\
	dpkgArch="$(dpkg --print-architecture)"; \
	case "$dpkgArch" in \
		ppc64el) \
# https://issues.apache.org/jira/browse/CASSANDRA-13345
# "The stack size specified is too small, Specify at least 328k"
			if grep -q -- '^-Xss' "$CASSANDRA_CONFIG/jvm.options"; then \
# 3.11+ (jvm.options)
				grep -- '^-Xss256k$' "$CASSANDRA_CONFIG/jvm.options"; \
				sed -ri 's/^-Xss256k$/-Xss512k/' "$CASSANDRA_CONFIG/jvm.options"; \
				grep -- '^-Xss512k$' "$CASSANDRA_CONFIG/jvm.options"; \
			elif grep -q -- '-Xss256k' "$CASSANDRA_CONFIG/cassandra-env.sh"; then \
# 3.0 (cassandra-env.sh)
				sed -ri 's/-Xss256k/-Xss512k/g' "$CASSANDRA_CONFIG/cassandra-env.sh"; \
				grep -- '-Xss512k' "$CASSANDRA_CONFIG/cassandra-env.sh"; \
			fi; \
			;; \
	esac; \
	\
# https://issues.apache.org/jira/browse/CASSANDRA-11661
	sed -ri 's/^(JVM_PATCH_VERSION)=.*/\1=25/' "$CASSANDRA_CONFIG/cassandra-env.sh"

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh /docker-entrypoint.sh # backwards compat
ENTRYPOINT ["docker-entrypoint.sh"]

RUN mkdir -p /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& chown -R cassandra:cassandra /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& chmod 777 /var/lib/cassandra "$CASSANDRA_CONFIG"
VOLUME /var/lib/cassandra

# 7000: intra-node communication
# 7001: TLS intra-node communication
# 7199: JMX
# 9042: CQL
# 9160: thrift service
EXPOSE 7000 7001 7199 9042 9160
CMD ["cassandra", "-f"]



```





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


# sha256sum ハッシュ値の確認



RUN ... && \
    wget -O [obj.tar.xz] [URL] && \
    echo " *** obj.tar.xz" | sha256sum -c && \
    mkdir -p [directory/obj] && \
    tar -xJf [obj.tar.xz] -C [directory/obj] && \
    rm [obj.tar.xz] && \
    cd [directory/obj]
    ...



キーワード



keyword


    "wget -O"
    "mkdir -p"
    "rm"
    "tar -xJf"
    "cd"

NG 

RUN ... && \
    wget -O [obj.tar.xz] [URL] && \
    mkdir -p [directory/obj] && \
    tar -xJf [obj.tar.xz] -C [directory/obj] && \
    rm [obj.tar.xz] && \
    cd [directory/obj]
    ...
    

NG


RUN ... && \
    wget -O [obj.tar.xz] [URL] && \
    mkdir -p [directory/obj] && \
    tar -xJf [obj.tar.xz] -C [directory/obj] && \
    cd [directory/obj]
    ...
    rm [obj-2.tar.xz] && \
    ...


NG 

RUN ... && \
    tar -xJf [obj.tar.xz] -C [directory/obj] && \
    cd [directory/obj]
    mkdir -p [directory/obj] && \
    wget -O [obj.tar.xz] [URL] && \
    rm [obj.tar.xz] && \
    ...


NG 

RUN ... && \
    wget -O [obj.tar.xz] [URL] && \
    mkdir -p [directory/obj] && \
    tar -xJf [obj.tar.xz] -C [directory/obj] && \
    rm [obj.tar.xz] && \
    cd [directory/obj]
    ...



NG

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






***

※1  set -ex \      ... ---> ['0.79100382', '0.20795377', '0.80418610', '...', '0.31484273']
※2  && buildDeps=' ... ---> ['0.20118536', '0.07181952', '0.49080551', '...', '0.23453401']
※3  && apt-get upda... ---> ['0.72694017', '0.74088527', '0.13279714', '...', '0.39210436']
※4  && apt-get inst... ---> ['0.60229535', '0.89038788', '0.05026947', '...', '0.64637082']



※2  && buildDeps=' ... ---> ['0.20118536', '0.07181952', '0.49080551', '...', '0.23453401']
※3  && apt-get upda... ---> ['0.72694017', '0.74088527', '0.13279714', '...', '0.39210436']
※4  && apt-get inst... ---> ['0.60229535', '0.89038788', '0.05026947', '...', '0.64637082']
※5  && rm -rf /var/... ---> ['0.06039495', '0.01400599', '0.49212851', '...', '0.69068759']



※8  && mkdir -p /us... ---> ['0.31146458', '0.93469031', '0.80601538', '...', '0.55286649']
※9  && tar -xJf rub... ---> ['0.98464268', '0.64775028', '0.18442020', '...', '0.15227497']
※10 && rm ruby.tar.... ---> ['0.80608755', '0.69243218', '0.82781117', '...', '0.96637163']
※11 && cd /usr/src/... ---> ['0.36719873', '0.39741394', '0.43383427', '...', '0.36633562']




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



※1  set -ex \      ...  |
※2  && buildDeps=' ...  |
※3  && apt-get upda...  | 
※4  && apt-get inst...  |   ['0.84677651', '0.92379878', '0.75155011', '...', '0.20286531']

※10 && rm ruby.tar....  | 
※11 && cd /usr/src/...  |





```






```bash

('ba805b53bf85b9b973529e6b258030334378c7fc:6', 0.7329501780604638)


query = [
        ['SC-WGET', 'SC-WGET-OUTPUT-DOCUMENT', 'BASH-PATH', 'BASH-LITERAL', 'ABS-MAYBE-PATH'],
        ['SC-WGET', 'SC-WGET-OUTPUT-DOCUMENT', 'BASH-PATH', 'BASH-LITERAL', 'ABS-PATH-ABSOLUTE'],
        ['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-PROBABLY-URL'],
        ['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-URL-PROTOCOL-HTTPS'],
        ['SC-WGET', 'SC-WGET-OUTPUT-DOCUMENT', 'BASH-PATH', 'BASH-LITERAL', 'ABS-MAYBE-PATH'],
        ['SC-WGET', 'SC-WGET-OUTPUT-DOCUMENT', 'BASH-PATH', 'BASH-LITERAL', 'ABS-PATH-ABSOLUTE'],
        ['SC-WGET', 'SC-WGET-OUTPUT-DOCUMENT', 'BASH-PATH', 'BASH-LITERAL', 'ABS-EXTENSION-ASC'],
        ['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-PROBABLY-URL'],
        ['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-URL-PROTOCOL-HTTPS'],
        ['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-EXTENSION-ASC'],
        ['SC-EXPORT', 'SC-EXPORT-TARGET', 'BASH-ASSIGN', 'BASH-ASSIGN-LHS', 'BASH-VARIABLE:GNUPGHOME'],
        ['SC-EXPORT', 'SC-EXPORT-TARGET', 'BASH-ASSIGN', 'BASH-ASSIGN-RHS', 'BASH-DOUBLE-QUOTED', 'BASH-DOLLAR-PARENS', 'SC-MKTEMP', 'SC-MKTEMP-F-DIRECTORY'],
        ['SC-GPG', 'SC-GPG-F-BATCH'],
        ['SC-GPG', 'SC-GPG-KEYSERVER', 'BASH-LITERAL', 'ABS-PROBABLY-URL'],
        ['SC-GPG', 'SC-GPG-KEYSERVER', 'BASH-LITERAL', 'ABS-URL-HA-POOL'],
        ['SC-GPG', 'SC-GPG-KEYSERVER', 'BASH-LITERAL', 'ABS-URL-POOL'],
        ['SC-GPG', 'SC-GPG-RECV-KEYS', 'SC-GPG-RECV-KEY', 'BASH-LITERAL'],
        ['SC-GPG', 'SC-GPG-F-BATCH'],
        ['SC-GPG', 'SC-GPG-VERIFYS', 'SC-GPG-VERIFY', 'BASH-LITERAL', 'ABS-MAYBE-PATH'],
        ['SC-GPG', 'SC-GPG-VERIFYS', 'SC-GPG-VERIFY', 'BASH-LITERAL', 'ABS-PATH-ABSOLUTE'],
        ['SC-GPG', 'SC-GPG-VERIFYS', 'SC-GPG-VERIFY', 'BASH-LITERAL', 'ABS-EXTENSION-ASC'],
        ['SC-GPG', 'SC-GPG-VERIFYS', 'SC-GPG-VERIFY', 'BASH-LITERAL', 'ABS-MAYBE-PATH'],
        ['SC-GPG', 'SC-GPG-VERIFYS', 'SC-GPG-VERIFY', 'BASH-LITERAL', 'ABS-PATH-ABSOLUTE'],
        ['SC-RM', 'SC-RM-F-RECURSIVE'],
        ['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL'],
        ['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-MAYBE-PATH'],
        ['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-PATH-ABSOLUTE'],
        ['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-EXTENSION-ASC'],
    ]





RUN set -ex \
	\
	&& wget -O python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
	&& wget -O python.tar.xz.asc "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
	&& gpg --batch --verify python.tar.xz.asc python.tar.xz \
	&& { command -v gpgconf > /dev/null && gpgconf --kill all || :; } \
	&& rm -rf "$GNUPGHOME" python.tar.xz.asc \
	&& mkdir -p /usr/src/python \
	&& tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
	&& rm python.tar.xz \
	\
	&& cd /usr/src/python \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	&& ./configure \
		--build="$gnuArch" \
		--enable-loadable-sqlite-extensions \
		--enable-shared \
		--with-system-expat \
		--with-system-ffi \
		--without-ensurepip \
	&& make -j "$(nproc)" \
	&& make install \
	&& ldconfig \
	\
	&& find /usr/local -depth \
		\( \
			\( -type d -a \( -name test -o -name tests \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' + \
	&& rm -rf /usr/src/python \
	\
	&& python3 --version


('bed9c0d43acadbd0e3b65c2f5f653ad0f7af0c05:1', 0.733756566010243)


['SC-APT-GET-UPDATE']
['SC-APT-GET-INSTALL', 'SC-APT-GET-F-YES']
['SC-APT-GET-INSTALL', 'SC-APT-GET-F-NO-INSTALL-RECOMMENDS']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:CA-CERTIFICATES']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:CURL']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:BUILD-ESSENTIAL']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:PKG-CONFIG']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:GIT']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:PYTHON']


RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		build-essential \
		pkg-config \
		git \
		python \
	&& rm -rf /var/lib/apt/lists/*

# verify gpg and sha256: http://nodejs.org/dist/v0.10.31/SHASUMS256.txt.asc
# gpg: aka "Timothy J Fontaine (Work) <tj.fontaine@joyent.com>"
RUN gpg --keyserver pool.sks-keyservers.net --recv-keys 7937DFD2AB06298B2293C3187D33FF9D0246406D

ENV NODE_VERSION 0.10.35
ENV NPM_VERSION 2.1.18

RUN curl -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
	&& curl -SLO "http://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
	&& gpg --verify SHASUMS256.txt.asc \
	&& grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - \
	&& tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
	&& rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc \
	&& npm install -g npm@"$NPM_VERSION" \
	&& npm cache clear

CMD [ "node" ]


('03d0ce54ce53227355e070a6d0d1ec1cdf986a29:10', 0.7560843477924944)

['SC-WGET', 'SC-WGET-OUTPUT-DOCUMENT', 'BASH-PATH', 'BASH-LITERAL', 'ABS-EXTENSION-TAR']
['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-PROBABLY-URL']
['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-URL-PROTOCOL-HTTPS']
['SC-WGET', 'SC-WGET-URL', 'BASH-LITERAL', 'ABS-EXTENSION-TAR']
['BASH-PIPELINE', 'SC-ECHO', 'SC-ECHO-ITEMS', 'SC-ECHO-ITEM', 'BASH-LITERAL', 'ABS-SINGLE-SPACE']
['BASH-PIPELINE', 'SC-ECHO', 'SC-ECHO-ITEMS', 'SC-ECHO-ITEM', 'BASH-LITERAL', 'ABS-EXTENSION-TAR']
['BASH-PIPELINE']
['SC-TAR', 'SC-TAR-X']
['SC-TAR', 'SC-TAR-V']
['SC-TAR', 'SC-TAR-FILE', 'BASH-PATH', 'BASH-LITERAL', 'ABS-EXTENSION-TAR']
['SC-TAR', 'SC-TAR-STRIP-COMPONENTS', 'BASH-LITERAL']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-EXTENSION-TAR']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-PROBABLY-URL']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-PROBABLY-URL']
['SC-MKDIR', 'SC-MKDIR-F-PARENTS']
['SC-MKDIR', 'SC-MKDIR-PATHS', 'SC-MKDIR-PATH', 'BASH-LITERAL']
['SC-MKDIR', 'SC-MKDIR-PATHS', 'SC-MKDIR-PATH', 'BASH-LITERAL']
['SC-MKDIR', 'SC-MKDIR-PATHS', 'SC-MKDIR-PATH', 'BASH-LITERAL']
['SC-MKDIR', 'SC-MKDIR-PATHS', 'SC-MKDIR-PATH', 'BASH-LITERAL']
['SC-MKDIR', 'SC-MKDIR-PATHS', 'SC-MKDIR-PATH', 'BASH-LITERAL']
['SC-CHOWN', 'SC-CHOWN-F-RECURSIVE']
['SC-CHOWN', 'SC-CHOWN-OWNER', 'BASH-LITERAL']
['SC-CHOWN', 'SC-CHOWN-PATHS', 'SC-CHOWN-PATH', 'BASH-LITERAL', 'ABS-MAYBE-PATH']
['SC-CHOWN', 'SC-CHOWN-PATHS', 'SC-CHOWN-PATH', 'BASH-LITERAL', 'ABS-PATH-RELATIVE']
['BASH-REDIRECT', 'BASH-REDIRECT-COMMAND', 'SC-ECHO', 'SC-ECHO-ITEMS', 'SC-ECHO-ITEM', 'BASH-LITERAL', 'ABS-SINGLE-SPACE']
['BASH-REDIRECT', 'BASH-REDIRECT-REDIRECTS', 'BASH-REDIRECT-OVERWRITE', 'BASH-PATH', 'BASH-LITERAL']
['SC-CHMOD', 'SC-CHMOD-F-RECURSIVE']
['SC-CHMOD', 'SC-CHMOD-MODE', 'BASH-LITERAL']
['SC-CHMOD', 'SC-CHMOD-PATHS', 'SC-CHMOD-PATH', 'BASH-LITERAL']
['SC-CHMOD', 'SC-CHMOD-PATHS', 'SC-CHMOD-PATH', 'BASH-LITERAL']
['SC-CHMOD', 'SC-CHMOD-PATHS', 'SC-CHMOD-PATH', 'BASH-LITERAL']



RUN wget -O redmine.tar.gz "https://www.redmine.org/releases/redmine-${REDMINE_VERSION}.tar.gz" \
	&& echo "$REDMINE_DOWNLOAD_MD5 redmine.tar.gz" | md5sum -c - \
	&& tar -xvf redmine.tar.gz --strip-components=1 \
	&& rm redmine.tar.gz files/delete.me log/delete.me \
	&& mkdir -p log public/plugin_assets sqlite tmp/pdf tmp/pids \
	&& chown -R redmine:redmine ./ \
# log to STDOUT (https://github.com/docker-library/redmine/issues/108)
	&& echo 'config.logger = Logger.new(STDOUT)' > config/additional_environment.rb \
# fix permissions for running as an arbitrary user
	&& chmod -R ugo=rwX config db sqlite \
	&& find log tmp -type d -exec chmod 1777 '{}' +


```



```bash



['SC-APT-GET-UPDATE']
['SC-APT-GET-UPDATE']
['SC-APT-GET-INSTALL', 'SC-APT-GET-F-YES']
['SC-APT-GET-INSTALL', 'SC-APT-GET-F-NO-INSTALL-RECOMMENDS']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:CA-CERTIFICATES']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:CURL']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES','SC-APT-GET-PACKAGE:BUILD-ESSENTIAL']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:PKG-CONFIG']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:GIT']
['SC-APT-GET-INSTALL', 'SC-APT-GET-PACKAGES', 'SC-APT-GET-PACKAGE:PYTHON']
['SC-RM', 'SC-RM-F-RECURSIVE']
['SC-RM', 'SC-RM-F-FORCE']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-MAYBE-PATH']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-PATH-ABSOLUTE']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-MAYBE-SRC-DIR']
['SC-RM', 'SC-RM-PATHS', 'SC-RM-PATH', 'BASH-LITERAL', 'ABS-USR-SRC-DIR']




RUN set -ex; \
	{ \
		echo "mariadb-server-$MARIADB_MAJOR" mysql-server/root_password password 'unused'; \
		echo "mariadb-server-$MARIADB_MAJOR" mysql-server/root_password_again password 'unused'; \
	} | debconf-set-selections; \
	apt-get update; \
	apt-get install -y \
		"mariadb-server=$MARIADB_VERSION" \
# mariadb-backup is installed at the same time so that `mysql-common` is only installed once from just mariadb repos
		mariadb-backup-10.2 \
		socat \
	; \
	rm -rf /var/lib/apt/lists/*; \
# comment out any "user" entires in the MySQL config ("docker-entrypoint.sh" or "--user" will handle user switching)
	sed -ri 's/^user\s/#&/' /etc/mysql/my.cnf /etc/mysql/conf.d/*; \
# purge and re-create /var/lib/mysql with appropriate ownership
	rm -rf /var/lib/mysql; \
	mkdir -p /var/lib/mysql /var/run/mysqld; \
	chown -R mysql:mysql /var/lib/mysql /var/run/mysqld; \
# ensure that /var/run/mysqld (used for socket and lock files) is writable regardless of the UID our mysqld instance ends up having at runtime
	chmod 777 /var/run/mysqld; \
# comment out a few problematic configuration values
	find /etc/mysql/ -name '*.cnf' -print0 \
		| xargs -0 grep -lZE '^(bind-address|log)' \
		| xargs -rt -0 sed -Ei 's/^(bind-address|log)/#&/'; \
# don't reverse lookup hostnames, they are usually another container
	echo '[mysqld]\nskip-host-cache\nskip-name-resolve' > /etc/mysql/conf.d/docker.cnf


```


```bash



RUN [A_1, A_2, A_3, A_4, A_5] && \
    [B_1, B_2, B_3, B_4, B_5] && \
    [C_1, C_2, C_3, C_4, C_5] && \
    [D_1, D_2, D_3, D_4, D_5] && \


    [A_1_1, A_1_2, A_1_3, A_1_4, A_1_5]
    [A_2_1, A_2_2, A_2_3]
    [A_3_1, A_3_2, A_3_3, A_3_4]
    [A_4_1, A_4_2, A_4_3, A_4_4, A_4_5]



    [A_2_1, A_2_2, A_2_3, A_2_2, A_2_1]




```


```bash



# vim:set ft=dockerfile:
FROM debian:stretch-slim

# explicitly set user/group IDs
RUN groupadd -r cassandra --gid=999 && \
	useradd -r -g cassandra --uid=999 cassandra

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
# solves warning: "jemalloc shared library could not be preloaded to speed up memory allocations"
		libjemalloc1 \
# free is used by cassandra-env.sh
		procps \
# "ip" is not required by Cassandra itself, but is commonly used in scripting Cassandra's configuration (since it is so fixated on explicit IP addresses)
		iproute2 \
	; \
	if ! command -v gpg > /dev/null; then \
		apt-get install -y --no-install-recommends \
			dirmngr \
			gnupg \
		; \
	fi; \
	rm -rf /var/lib/apt/lists/*

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.10
RUN set -x \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends ca-certificates wget \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& { command -v gpgconf && gpgconf --kill all || :; } \
	&& rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apt-get purge -y --auto-remove ca-certificates wget
	


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


※1  set -ex \      ... --> vec_1 :['0.79100382', '0.20795377', '0.80418610', '...', '0.31484273']
※2  && buildDeps=' ... --> vec_2 :['0.20118536', '0.07181952', '0.49080551', '...', '0.23453401']
※3  && apt-get upda... --> vec_3 :['0.72694017', '0.74088527', '0.13279714', '...', '0.39210436']
※4  && apt-get inst... --> vec_4 :['0.60229535', '0.89038788', '0.05026947', '...', '0.64637082']
※5  && rm -rf /var/... --> vec_5 :['0.06039495', '0.01400599', '0.49212851', '...', '0.69068759']
※6  && wget -O ruby... --> vec_6 :['0.47584121', '0.22825153', '0.99073123', '...', '0.52057977']
※7  && echo '$RUBY_... --> vec_7 :['0.32533716', '0.17752849', '0.36939683', '...', '0.22831389']
※8  && mkdir -p /us... --> vec_8 :['0.31146458', '0.93469031', '0.80601538', '...', '0.55286649']
※9  && tar -xJf rub... --> vec_9 :['0.98464268', '0.64775028', '0.18442020', '...', '0.15227497']
※10 && rm ruby.tar.... --> vec_10:['0.80608755', '0.69243218', '0.82781117', '...', '0.96637163']
※11 && cd /usr/src/... --> vec_11:['0.36719873', '0.39741394', '0.43383427', '...', '0.36633562']


※1  set -ex \      ... --> cmd_vec_1 :['0.79100382', '0.20795377', '...', '0.31484273']
※2  && buildDeps=  ... --> cmd_vec_2 :['0.20118536', '0.07181952', '...', '0.23453401']
※3  && apt-get upda... --> cmd_vec_3 :['0.72694017', '0.74088527', '...', '0.39210436']
※4  && apt-get inst... --> cmd_vec_4 :['0.60229535', '0.89038788', '...', '0.64637082']
※5  && rm -rf /var/... --> cmd_vec_5 :['0.06039495', '0.01400599', '...', '0.69068759']
※6  && wget -O ruby... --> cmd_vec_6 :['0.47584121', '0.22825153', '...', '0.52057977']
※7  && echo  $RUBY_... --> cmd_vec_7 :['0.32533716', '0.17752849', '...', '0.22831389']
※8  && mkdir -p /us... --> cmd_vec_8 :['0.31146458', '0.93469031', '...', '0.55286649']
※9  && tar -xJf rub... --> cmd_vec_9 :['0.98464268', '0.64775028', '...', '0.15227497']
※10 && rm ruby.tar.... --> cmd_vec_10:['0.80608755', '0.69243218', '...', '0.96637163']
※11 && cd /usr/src/... --> cmd_vec_11:['0.36719873', '0.39741394', '...', '0.36633562']


※1  set -ex \      ... --> vec_1 :
※2  && buildDeps=  ... --> vec_2 :
※3  && apt-get upda... --> vec_3 :
※4  && apt-get inst... --> vec_4 :
※5  && rm -rf /var/... --> vec_5 :
※6  && wget -O ruby... --> vec_6 :
※7  && echo  $RUBY_... --> vec_7 :
※8  && mkdir -p /us... --> vec_8 :
※9  && tar -xJf rub... --> vec_9 :
※10 && rm ruby.tar.... --> vec_10:
※11 && cd /usr/src/... --> vec_11:


※1  set -ex \      ... --> 
※2  && buildDeps=  ... --> 
※3  && apt-get upda... --> 
※4  && apt-get inst... -->
※5  && rm -rf /var/... --> 
※6  && wget -O ruby... --> run_vec_* :['0.84677651', '0.92379878', '...', '0.20286531']
※7  && echo  $RUBY_... -->  
※8  && mkdir -p /us... --> 
※9  && tar -xJf rub... --> 
※10 && rm ruby.tar.... --> 
※11 && cd /usr/src/... --> 

※1  set -ex \      ... -| 
※2  && buildDeps=' ... -| 
※3  && apt-get upda... -| 
※4  && apt-get inst... -| 
※5  && rm -rf /var/... -| 
※6  && wget -O ruby... -|-> vec_*: ['0.84677651', '0.92379878', '...', '0.20286531']
※7  && echo '$RUBY_... -| 
※8  && mkdir -p /us... -| 
※9  && tar -xJf rub... -| 
※10 && rm ruby.tar.... -| 
※11 && cd /usr/src/... -| 


※1  set -ex \      ... : -- vec_1 --> 
※2  && buildDeps=' ... : -- vec_2 --> 
※3  && apt-get upda... : -- vec_3 --> 
※4  && apt-get inst... : -- vec_4 --> 
※5  && rm -rf /var/... : -- vec_5 --> 
※6  && wget -O ruby... : -- vec_6 --> 
※7  && echo '$RUBY_... : -- vec_7 --> 
※8  && mkdir -p /us... : -- vec_8 --> 
※9  && tar -xJf rub... : -- vec_9 --> 
※10 && rm ruby.tar.... : -- vec_10--> 
※11 && cd /usr/src/... : -- vec_11--> 


[※1 set -ex \   ...]
[※2 buildDeps=  ...]
[※3 apt-get upda...]
[※4 apt-get inst...]
[※5 rm -rf /var/...]
[※6 wget -O ruby...]

[※1 set -ex \   ...][※1 set -ex \   ...][※1 set -ex \   ...][※1 set -ex \   ...]


[※3 apt-get upda...][※3 apt-get upda...][※3 apt-get upda...][※3 apt-get upda...] --> [※3 apt-get upda...]


["          "]["cmd_vec_1 "]["cmd_vec_2 "]["cmd_vec_3 "]              ["run_vec_* "]
["cmd_vec_1 "]["cmd_vec_2 "]["cmd_vec_3 "]["cmd_vec_4 "]              ["run_vec_* "]
["cmd_vec_2 "]["cmd_vec_3 "]["cmd_vec_4 "]["cmd_vec_5 "]              ["run_vec_* "]
["cmd_vec_3 "]["cmd_vec_4 "]["cmd_vec_5 "]["cmd_vec_6 "]              ["run_vec_* "]


["cmd_vec_6 "]["cmd_vec_7 "]["cmd_vec_8 "]["cmd_vec_9 "]              ["run_vec_* "]
["cmd_vec_7 "]["cmd_vec_8 "]["cmd_vec_9 "]["cmd_vec_10"]              ["run_vec_* "]



["          "]["cmd_vec_1 "]["cmd_vec_2 "]["cmd_vec_3 "] --> ["run_vec_* "]
["cmd_vec_1 "]["cmd_vec_2 "]["cmd_vec_3 "]["cmd_vec_4 "] --> ["run_vec_* "]
["cmd_vec_2 "]["cmd_vec_3 "]["cmd_vec_4 "]["cmd_vec_5 "] --> ["run_vec_* "]
["cmd_vec_3 "]["cmd_vec_4 "]["cmd_vec_5 "]["cmd_vec_6 "] --> ["run_vec_* "]


["cmd_vec_6 "]["cmd_vec_7 "]["cmd_vec_8 "]["cmd_vec_9 "] --> ["run_vec_* "]
["cmd_vec_7 "]["cmd_vec_8 "]["cmd_vec_9 "]["cmd_vec_10"] --> ["run_vec_* "]




[-- vec_1 -->][-- vec_1 -->][-- vec_1 -->][-- vec_1 -->] --> [-- vec_1 -->]

["-- vec_1 -->"]["-- vec_2 -->"]["-- vec_3 -->"]["-- vec_4 -->"] --> ["-- vec_5 -->"]
["-- vec_2 -->"]["-- vec_3 -->"]["-- vec_4 -->"]["-- vec_5 -->"] --> ["-- vec_6 -->"]







※1  set -ex \      ... ---> ['0.79100382', '0.20795377', '0.80418610', '...', '0.31484273']
														 -- vec_1 --> 
※2  && buildDeps=' ... ---> ['0.20118536', '0.07181952', '0.49080551', '...', '0.23453401']
														 -- vec_2 --> 
※3  && apt-get upda... ---> ['0.72694017', '0.74088527', '0.13279714', '...', '0.39210436']
														 -- vec_3 --> 
※4  && apt-get inst... ---> ['0.60229535', '0.89038788', '0.05026947', '...', '0.64637082']
														 -- vec_4 --> 
※5  && rm -rf /var/... ---> ['0.06039495', '0.01400599', '0.49212851', '...', '0.69068759']
														 -- vec_5 --> 
※6  && wget -O ruby... ---> ['0.47584121', '0.22825153', '0.99073123', '...', '0.52057977']
														 -- vec_6 --> 
※7  && echo '$RUBY_... ---> ['0.32533716', '0.17752849', '0.36939683', '...', '0.22831389']
														 -- vec_7 --> 
※8  && mkdir -p /us... ---> ['0.31146458', '0.93469031', '0.80601538', '...', '0.55286649']
														 -- vec_8 --> 
※9  && tar -xJf rub... ---> ['0.98464268', '0.64775028', '0.18442020', '...', '0.15227497']
														 -- vec_9 --> 
※10 && rm ruby.tar.... ---> ['0.80608755', '0.69243218', '0.82781117', '...', '0.96637163']
														 -- vec_10--> 
※11 && cd /usr/src/... ---> ['0.36719873', '0.39741394', '0.43383427', '...', '0.36633562']
														 -- vec_11--> 





※2  && buildDeps=  ... --> ['0.20118536', '0.07181952', '...', '0.23453401']
※3  && apt-get upda... --> ['0.72694017', '0.74088527', '...', '0.39210436']
※4  && apt-get inst... --> ['0.60229535', '0.89038788', '...', '0.64637082']
※5  && rm -rf /var/... --> ['0.06039495', '0.01400599', '...', '0.69068759']


※1  && wget -O ruby... --> query_vec_1 :['0.47584121', '0.22825153', '...', '0.52057977']
※2  && echo  $RUBY_... --> query_vec_2 :['0.32533716', '0.17752849', '...', '0.22831389']
※3  && mkdir -p /us... --> query_vec_3 :['0.31146458', '0.93469031', '...', '0.55286649']
※4  && tar -xJf rub... --> query_vec_4 :['0.98464268', '0.64775028', '...', '0.15227497']


RUN
	...
	&& wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	&& mkdir -p /usr/src/ruby \
	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
	&& rm ruby.tar.xz \
	...

※query_1 : < wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" >
※query_2 : < echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - >
※query_3 : < mkdir -p /usr/src/ruby >
※query_4 : < tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 >

※vec_1   :['0.47584121', '0.22825153', '...', '0.52057977']
※vec_2   :['0.32533716', '0.17752849', '...', '0.22831389']
※vec_3   :['0.31146458', '0.93469031', '...', '0.55286649']
※vec_4   :['0.98464268', '0.64775028', '...', '0.15227497']


※out_vec :['0.32533716', '0.17752849', '...', '0.22831389']


URL  : https?://[\w!\?/\+\-_~=;\.,\*&@#\$%\(\)'\[\]]+
Email: [\w\-\._]+@[\w\-\._]+\.[A-Za-z]+


grep "wget -O" | 
\ grep "mkdir -p" | 
\ grep "rm" | 
\ grep "tar -xJf" | 
\ grep "cd" -rl ./deduplicated-sources-gold  | wc -l



~/D/leagal ❯❯❯ grep "wget -O" | grep "mkdir -p" | grep "rm" | grep "tar -xJf" | grep "cd"  -rl ./deduplicated-sources-gold                               ✘ 127
./deduplicated-sources-gold/d0a7a33cad90bc506788da62fe4617372159cce0.Dockerfile
./deduplicated-sources-gold/3da1e5be2520174f22c0f29a0078e49569be151d.Dockerfile
./deduplicated-sources-gold/486c95e2e24a4cdccecf405cf316cd643824650e.Dockerfile
./deduplicated-sources-gold/6bdc46f23236f247a7df69d0a1a529354924df04.Dockerfile
./deduplicated-sources-gold/6e482708d3cafd1b0361e981702a95b023033688.Dockerfile
./deduplicated-sources-gold/cd636feca30c0fecd812864b5381dd5d16c8e15a.Dockerfile
./deduplicated-sources-gold/ea454ad2a9a42446cb9c57497d05b72d04de1249.Dockerfile
./deduplicated-sources-gold/73862997d0efd4fe0044d1385cde7fb4e7effba4.Dockerfile
./deduplicated-sources-gold/2f4b9caf535bcc4fe1ce72c621240d5c89fe0411.Dockerfile
./deduplicated-sources-gold/21bc31687e218b23614520b7e818ae64f5f3de69.Dockerfile
./deduplicated-sources-gold/603297d09551b7f42450566eb16dc1682c5a4aed.Dockerfile
./deduplicated-sources-gold/a27c7d503a860f701d00c563ed695af03a5df72d.Dockerfile
./deduplicated-sources-gold/587a179b228c2b592f30f09d42a1197d853dd665.Dockerfile
./deduplicated-sources-gold/41d711ae650a667318ebf53c9ba3d5bbdb9bb892.Dockerfile
./deduplicated-sources-gold/7abb94f2128445d47f90dff64fb8af6aa148deed.Dockerfile
./deduplicated-sources-gold/217c60ffbc22133df5fc6cffa99426d1b552889d.Dockerfile
./deduplicated-sources-gold/696f61780cc05c8c2600f87f58a6eee8749d29fe.Dockerfile
./deduplicated-sources-gold/57e226605bfd29c975c229d29d2ed5bd7f48afe4.Dockerfile
./deduplicated-sources-gold/c8f7e39cc87328ebd91d63dbc764ad7d73be3be9.Dockerfile
./deduplicated-sources-gold/a8f77acefc49fc3cd97ae0fd6cbdf3c18212dc67.Dockerfile
./deduplicated-sources-gold/f5cb1dcf6e839e51e9440c761838df24ec697e7f.Dockerfile
./deduplicated-sources-gold/2822cecdbb823c5ad6be5072deb79c14eb5959fb.Dockerfile
./deduplicated-sources-gold/8a96f06d7db90215d7dd133b8cc40e1e961152df.Dockerfile
./deduplicated-sources-gold/cb7d8e3b16a8e5273808c27db2d73bff8a6717e3.Dockerfile
./deduplicated-sources-gold/08faf411c5d4601b944a817c4180f94bed33adb2.Dockerfile
./deduplicated-sources-gold/46146eb0c2ad8dccdf2df8ee87c89605a3180a3d.Dockerfile



※query_1 : < wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" >
※query_2 : < echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - >
※query_3 : < mkdir -p /usr/src/ruby >
※query_4 : < tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 >







※vec_1   :['0.47584121', '0.22825153', '...', '0.52057977']
※vec_2   :['0.32533716', '0.17752849', '...', '0.22831389']
※vec_3   :['0.31146458', '0.93469031', '...', '0.55286649']
※vec_4   :['0.98464268', '0.64775028', '...', '0.15227497']







※out_vec :['0.32533716', '0.17752849', '...', '0.22831389']







※rank1   :('a8f77acefc49fc3cd97ae0fd6cbdf3c18212dc67:3', 0.771160364151001)
※rank2   :('03d0ce54ce53227355e070a6d0d1ec1cdf986a29:10', 0.7534516453742981)
※rank3   :('935fe6457daa80a4725e0e2bcd21db4bdd37cc8f:9', 0.7330055236816406)
※rank4   :('3c3a790c2d100c1a02147c2917f018290135bf79:2', 0.7328020334243774)
※rank5   :('a31b702830630aec34c396f7bdcbaf7705bb19ac:3', 0.7326844930648804)
※rank6   :('c7dceeceb6a3dbedd26e1243868b82426711a4b1:4', 0.7316206097602844)
※rank7   :('563edde6aed306c2ec107283e34155b7757c56dd:4', 0.7295385599136353)
※rank8   :('5ee4ebe99baccc7ac504582d3ac820038862f479:1', 0.728958010673523)
※rank9   :('cb159711f8fc0f0e82c1eeaca66744a7e11f41bc:2', 0.7215109467506409)
※rank10  :('027de8dd9fb86c52209cb18af272ab6958a5eae5:7', 0.7181053161621094)

```
