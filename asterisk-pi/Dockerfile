FROM navikey/raspbian-bullseye
RUN  true \
&& cat /etc/os-release \
&& apt-get update \
&& apt-get upgrade -y 

WORKDIR /usr/local/src
RUN true \
&& wget https://downloads.asterisk.org/pub/telephony/asterisk/releases/asterisk-20.1.0.tar.gz \
&& tar -zxvf asterisk-20.1.0.tar.gz 


WORKDIR /usr/local/src/asterisk-20.1.0/contrib/scripts

RUN true \
&& ./install_prereq install


WORKDIR /usr/local/src/asterisk-20.1.0
RUN true \
&& ./configure
RUN make menuselect.makeopts
RUN menuselect/menuselect --enable format_mp3 --enable CORE-SOUNDS-EN-WAV --enable CORE-SOUNDS-RU-GSM --enable CORE-SOUNDS-RU-WAV menuselect.makeopts
RUN make
RUN contrib/scripts/get_mp3_source.sh 
RUN make install  
RUN make samples
RUN make config
RUN make install-logrotate