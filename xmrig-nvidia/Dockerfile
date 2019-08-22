FROM nvidia/cuda:9.2-devel-ubuntu18.04

ENV CMAKE_OPTS='-DCMAKE_C_COMPILER=gcc-7 -DCMAKE_CXX_COMPILER=g++-7 -DWITH_HTTPD=OFF'

RUN set -x \
    && apt-get -y update \
    && apt-get -y install git build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev \
    && git clone https://github.com/xmrig/xmrig-nvidia.git \
    && cd xmrig-nvidia \
    && sed -i 's/constexpr const int kDefaultDonateLevel = 5;/constexpr const int kDefaultDonateLevel = 0;/' src/donate.h \
    && sed -i 's/constexpr const int kMinimumDonateLevel = 1;/constexpr const int kMinimumDonateLevel = 0;/' src/donate.h \
    && mkdir build \
    && cd build \
    && cmake .. -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda -DCUDA_LIB=/usr/local/cuda/compat/libcuda.so ${CMAKE_OPTS} \
    && make