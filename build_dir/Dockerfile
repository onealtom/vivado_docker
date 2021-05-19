FROM dorowu/ubuntu-desktop-lxde-vnc:bionic

MAINTAINER Oneal Tang <tyf@vavitel.com>

# build cmd: docker build --build-arg VIVADO_TAR_HOST=http://ip:5000 --build-arg VIVADO_TAR_FILE=Xilinx_Vivado_2019.2_1106_2127 -t vivado2019_2 .

#install dependences for:
# * downloading Vivado (wget)
# * xsim (gcc build-essential to also get make)
# * MIG tool (libglib2.0-0 libsm6 libxi6 libxrender1 libxrandr2 libfreetype6 libfontconfig)
# * CI (git)
#ADD sources.list /etc/apt/

RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
  wget \
  build-essential \
  git \
  make \
  lib32ncurses5 lib32z1 \
  libssl-dev \
  libelf-dev

# download and run the install
ARG VIVADO_TAR_HOST
ARG VIVADO_TAR_FILE
#ARG VIVADO_VERSION
ARG VIVADO_INSTALL_DIR="/home/vivado/setup"

RUN adduser --disabled-password --gecos '' vivado

RUN mkdir -p /home/vivado/workspace
RUN mkdir -p /home/vivado/setup
RUN mkdir -p /home/vivado/licdir

RUN chown vivado /home/vivado
RUN chown vivado /home/vivado/workspace
RUN chown vivado /home/vivado/setup
RUN chown vivado /home/vivado/licdir

RUN chown vivado /opt
RUN chmod +w /opt

USER vivado

COPY Xilinx.lic /home/vivado/licdir

COPY install_config.txt ${VIVADO_INSTALL_DIR}/

RUN cd ${VIVADO_INSTALL_DIR} && echo "Downloading ${VIVADO_TAR_FILE} from ${VIVADO_TAR_HOST}" && \
  wget ${VIVADO_TAR_HOST}/${VIVADO_TAR_FILE}.tar.gz -q && \
  echo "Extracting Vivado tar file" && \
  tar xzf ${VIVADO_TAR_FILE}.tar.gz && \
  ${VIVADO_INSTALL_DIR}/${VIVADO_TAR_FILE}/xsetup --agree 3rdPartyEULA,WebTalkTerms,XilinxEULA --batch Install --config ${VIVADO_INSTALL_DIR}/install_config.txt && \
  rm -rf ${VIVADO_INSTALL_DIR}/${VIVADO_TAR_FILE}* 

ENV PATH="/opt/Xilinx/Vivado/2019.2/bin:/opt/Xilinx/SDK/2019.2/bin:/opt/Xilinx/SDK/2019.2/gnu/microblaze/lin/bin:/opt/Xilinx/SDK/2019.2/gnu/arm/lin/bin:/opt/Xilinx/SDK/2019.2/gnu/microblaze/linux_toolchain/lin64_le/bin:/opt/Xilinx/SDK/2019.1/gnu/aarch32/lin/gcc-arm-linux-gnueabi/bin:/opt/Xilinx/SDK/2019.2/gnu/aarch32/lin/gcc-arm-none-eabi/bin:/opt/Xilinx/SDK/2019.2/gnu/aarch64/lin/aarch64-linux/bin:/opt/Xilinx/SDK/2019.2/gnu/aarch64/lin/aarch64-none/bin:/opt/Xilinx/SDK/2019.2/gnu/armr5/lin/gcc-arm-none-eabi/bin:/opt/Xilinx/SDK/2019.2/tps/lnx64/cmake-3.3.2/bin:${PATH}"

#COPY Xilinx.lic /home/vivado/.Xilinx/
COPY Xilinx.lic /home/vivado/licdir/
ENV XILINXD_LICENSE_FILE="/home/vivado/licdir"
ENV LM_LICENSE_FILE="/home/vivado/licdir"
