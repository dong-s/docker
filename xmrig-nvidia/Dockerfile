ARG CUDA_VERSION=9.2
ARG BUILD_FLAVOR=devel
ARG RUN_FLAVOR=base
ARG DISTRO=ubuntu18.04

FROM nvidia/cuda:${CUDA_VERSION}-${BUILD_FLAVOR}-${DISTRO} AS build

RUN set -x \
    && apt-get -y update \
    && apt-get -y install git build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev \
    && git clone https://github.com/xmrig/xmrig-nvidia.git \
    && cd xmrig-nvidia \
    && sed -i 's/constexpr const int kDefaultDonateLevel = 5;/constexpr const int kDefaultDonateLevel = 0;/' src/donate.h \
    && sed -i 's/constexpr const int kMinimumDonateLevel = 1;/constexpr const int kMinimumDonateLevel = 0;/' src/donate.h \
    && mkdir build \
    && cd build \
    && cmake .. -DCUDA_LIB=/usr/local/cuda ${CMAKE_OPTS} \
    && make

FROM nvidia/cuda:${CUDA_VERSION}-${RUN_FLAVOR}-${DISTRO}

COPY --from=build /xmrig-nvidia/build/xmrig-nvidia /usr/local/bin/xmrig-nvidia

CMD ["xmrig-nvidia"]