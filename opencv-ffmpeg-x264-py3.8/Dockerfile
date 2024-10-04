FROM python:3.8

WORKDIR /app

# af of this writing this landed at commit baee400fa9ced6f5481a728138fed6e867b0ff7f
RUN apt-get -qq update \
	&& apt-get -qq install nasm \
	&& git clone https://code.videolan.org/videolan/x264.git \
	&& cd x264 \
	&& git checkout stable \
	&& ./configure --enable-static --enable-shared \
	&& make install

RUN wget https://ffmpeg.org/releases/ffmpeg-5.0.1.tar.xz \
	&& tar Jxf ./ffmpeg-5.0.1.tar.xz \
	&& cd ffmpeg-5.0.1 \
	&& ./configure --enable-shared --enable-nonfree --enable-gpl --enable-libx264 \
	&& make install

# Release 4.6.0.66 https://github.com/opencv/opencv-python/releases/tag/66
RUN git clone https://github.com/opencv/opencv-python.git \
	&& cd opencv-python \
	&& git checkout 66 \
	&& ENABLE_HEADLESS=1 pip3.8 wheel . \
	&& pip3.8 install opencv_python_headless-4.6.0.66-cp38-cp38-linux_x86_64.whl

ENV LD_LIBRARY_PATH=/usr/local/lib
