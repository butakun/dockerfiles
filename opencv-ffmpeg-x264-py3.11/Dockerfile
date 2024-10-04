FROM python:3.11

WORKDIR /build

RUN apt-get -qq update \
	&& apt-get -qq install nasm \
	&& git clone https://code.videolan.org/videolan/x264.git \
	&& cd x264 \
	&& git checkout c24e06c2e184345ceb33eb20a15d1024d9fd3497 \
	&& ./configure --enable-static --enable-shared \
	&& make install

RUN wget https://ffmpeg.org/releases/ffmpeg-7.1.tar.xz \
	&& tar Jxf ./ffmpeg-7.1.tar.xz \
	&& cd ffmpeg-7.1 \
	&& ./configure --enable-shared --enable-nonfree --enable-gpl --enable-libx264 \
	&& make install

# Release 4.10.0.84 https://github.com/opencv/opencv-python/releases/tag/84
RUN git clone https://github.com/opencv/opencv-python.git \
	&& cd opencv-python \
	&& git checkout 84 \
	&& ENABLE_HEADLESS=1 pip3.11 wheel . \
	&& pip3.11 install opencv_python_headless-4.10.0.84-cp311-cp311-linux_x86_64.whl

ENV LD_LIBRARY_PATH=/usr/local/lib

ENTRYPOINT ["/usr/local/bin/python"]
