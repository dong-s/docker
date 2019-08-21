FROM merxnet/xmr-stak-nvidia:dev
ENV CMAKE_OPTS -DXMR-STAK_COMPILE=generic -DCUDA_ENABLE=ON -DOpenCL_ENABLE=OFF -DMICROHTTPD_ENABLE=OFF -DHWLOC_ENABLE=OFF

WORKDIR /home

RUN apt-get update \
    && apt-get -y install --no-install-recommends cmake g++ gcc git libc++-dev libssl-dev make \
    && git clone https://github.com/fireice-uk/xmr-stak.git \
    && cd xmr-stak \
    && sed -i 's/constexpr double fDevDonationLevel.*/constexpr double fDevDonationLevel = 0.0;/' xmrstak/donate-level.hpp \
    && mkdir build \
    && cd build \
    && cmake .. ${CMAKE_OPTS} \
    && make install
