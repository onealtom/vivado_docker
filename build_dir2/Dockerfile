FROM registry.cn-shenzhen.aliyuncs.com/cangcanglang/vivado2019p2:v1

MAINTAINER Oneal Tang <tyf@vavitel.com>

# build cmd: docker build --build-arg XSCT_TAR_HOST=http://192.168.3.247:5000 --build-arg XSCT_TAR_FILE=xsct_2019.2.tar.xz -t registry.cn-shenzhen.aliyuncs.com/cangcanglang/vivado2019p2:v2 .

ARG XSCT_TAR_HOST
ARG XSCT_TAR_FILE

WORKDIR /home/vivado/workspace
RUN wget ${XSCT_TAR_HOST}/${XSCT_TAR_FILE} -q && \
  tar -xf ${XSCT_TAR_FILE} -C /opt/Xilinx/ && \
  rm -rf ${XSCT_TAR_FILE}

ENV PATH="/opt/Xilinx/Vivado/2019.2/bin:/opt/Xilinx/Vitis/2019.2/bin:/opt/Xilinx/Vitis/2019.2/gnu/aarch32/lin/gcc-arm-none-eabi/bin:/opt/Xilinx/Vitis/2019.2/gnu/aarch64/lin/aarch64-none/bin:/opt/Xilinx/Vitis/2019.2/gnu/armr5/lin/gcc-arm-none-eabi/bin:/opt/Xilinx/Vitis/2019.2/gnu/microblaze/lin/bin:/opt/Xilinx/Vitis/2019.2/tps/lnx64/cmake-3.3.2/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
