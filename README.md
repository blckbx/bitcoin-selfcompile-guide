# How to self-compile Bitcoin client (libre-relay)

1) Install dependencies

```
$ sudo apt install -y \
    build-essential \
    cmake \
    libboost-all-dev \
    libevent-dev \
    libtool \
    pkg-config \
    libzmq3-dev \
    libsqlite3-dev \
    libminiupnpc-dev \
    libnatpmp-dev
```

2) Clone repository

```
$ git clone https://github.com/petertodd/bitcoin.git libre-relay
$ cd libre-relay
$ git checkout libre-relay-v29.0
```

3) Create build dir

```
$ mkdir -p build/bin
```

4) Configure

```
$ cmake -B build \
  -DCMAKE_INSTALL_PREFIX=/build \
  -DINSTALL_MAN=OFF \
  -DBUILD_SHARED_LIBS=OFF \
  -DWITH_CCACHE=OFF \
  -DBUILD_TESTS=OFF \
  -DREDUCE_EXPORTS=ON \
  -DBUILD_UTIL=ON \
  -DBUILD_WALLET_TOOL=ON \
  -DWITH_ZMQ=ON
```

5) Build

```
$ cmake --build build -j$(nproc)
```

6) Install

```
$ sudo install -m 0755 -o root -g root -t /usr/local/bin/ /build/bin/*
```

7) Run

```
$ bitcoind --version

> Bitcoin Core daemon version libre-relay-v29.0-2
```
