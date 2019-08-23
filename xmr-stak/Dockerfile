ARG CUDA_VERSION=10.1
ARG BUILD_FLAVOR=devel
ARG RUN_FLAVOR=runtime
ARG DISTRO=ubuntu18.04

FROM nvidia/cuda:${CUDA_VERSION}-${BUILD_FLAVOR}-${DISTRO} AS build

ENV CMAKE_OPTS '-DMICROHTTPD_ENABLE=OFF -DXMR-STAK_COMPILE=generic -DHWLOC_ENABLE=ON -DCPU_ENABLE=ON -DOpenCL_ENABLE=OFF'

RUN set -x \
    && apt-get update \
    && apt-get -y install --no-install-recommends cmake g++ gcc git libc++-dev libssl-dev make libhwloc-dev\
    && git clone https://github.com/fireice-uk/xmr-stak.git \
    && cd xmr-stak \
    && sed -i 's/constexpr double fDevDonationLevel.*/constexpr double fDevDonationLevel = 0.0;/' xmrstak/donate-level.hpp \
    && mkdir build \
    && cd build \
    && cmake .. ${CMAKE_OPTS} \
    && make install

FROM nvidia/cuda:${CUDA_VERSION}-${RUN_FLAVOR}-${DISTRO}

COPY --from=build /xmr-stak/build/bin/* /usr/local/bin/

RUN apt-get update \
    && apt-get -y install --no-install-recommends libhwloc-dev

WORKDIR /usr/local/bin

CMD ["xmr-stak"]
