ARG CUDA_VERSION=10.1
ARG BUILD_FLAVOR=devel
ARG RUN_FLAVOR=base
ARG DISTRO=ubuntu18.04

FROM nvidia/cuda:${CUDA_VERSION}-${BUILD_FLAVOR}-${DISTRO} AS build

ENV CMAKE_OPTS='-DCMAKE_C_COMPILER=gcc-7 -DCMAKE_CXX_COMPILER=g++-7 -DWITH_AEON=OFF -DWITH_HTTPD=OFF'

RUN apt-get -y update \
    && apt-get -y install git build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev \
    && git clone https://github.com/xmrig/xmrig-nvidia.git \
    && cd xmrig-nvidia \
    && sed -i 's/constexpr const int kDefaultDonateLevel = 5;/constexpr const int kDefaultDonateLevel = 0;/' src/donate.h \
    && sed -i 's/constexpr const int kMinimumDonateLevel = 1;/constexpr const int kMinimumDonateLevel = 0;/' src/donate.h \
    && mkdir build \
    && cmake .. -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda ${CMAKE_OPTS} \
    && make

FROM nvidia/cuda:${CUDA_VERSION}-${RUN_FLAVOR}-${DISTRO}

COPY --from=build /xmrig-nvidia/build/xmrig-nvidia /usr/local/bin/xmrig-nvidia

CMD ["xmrig-nvidia"]