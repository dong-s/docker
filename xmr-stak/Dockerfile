ARG CUDA_VERSION=9.2
ARG BUILD_FLAVOR=devel
ARG RUN_FLAVOR=base
ARG DISTRO=ubuntu18.04

FROM nvidia/cuda:${CUDA_VERSION}-${BUILD_FLAVOR}-${DISTRO} AS build

ENV CMAKE_OPTS -DXMR-STAK_COMPILE=generic -DCUDA_ENABLE=ON -DOpenCL_ENABLE=OFF -DMICROHTTPD_ENABLE=OFF

RUN apt-get update \
    && apt-get -y install --no-install-recommends cmake g++ gcc git libc++-dev libssl-dev make \
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
    && apt-get -y install --no-install-recommends gcc libc++1

WORKDIR /usr/local/bin
