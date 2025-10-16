# How to self-compile Bitcoin

```
sudo apt install -y \
    build-essential \
    cmake \
    libboost-all-dev \
    libevent-dev \
    libtool \
    pkg-config \
    libzmq3-dev \
    libsqlite3-dev \
    libminiupnpc-dev \
    libnatpmp-dev \
    libcapnp-dev \
    capnproto
```
```
curl -s "https://api.github.com/repos/bitcoin-core/guix.sigs/contents/builder-keys" | \
jq -r '.[].download_url' | while read url; do curl -s "$url" | gpg --import; done
```
```
git clone https://github.com/bitcoin/bitcoin.git && \ 
cd bitcoin
```
```
git checkout v30.0 && \
git verify-tag v30.0
```
```
mkdir -p build/bin
```
```
cmake -B build \
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
```
cmake --build build -j$(nproc)
```
```
strip build/bin/*
```
```
sudo install -m 0755 -o root -g root -t /usr/local/bin/ build/bin/*
```
```
bitcoind --version
> Bitcoin Core daemon version v30.0
```
