# RaspberryPi
<img src="/RPI_Camera.png" width="40%" height="40%"></br>
HTTP 서버와 RTSP 서버 중 하나의 서버를 선택해서 설치하세요.
둘 중에 하나를 택한뒤 다른 서버를 테스트해보고 싶을 시 포맷을 하고 시도 해주세요.


# HTTP Server
<li>HLS(http live streaming)</li>
<li>MPEG-DASH</li>

## Usage
### Streaming video from the Raspberry Pi with mjpg-streamer
<code>sudo rpi-update</code></br>
<code>sudo apt-get update</code></br>
<code>sudo apt-get upgrade</code></br>
<code>sudo mkdir /home/pi/mjpg-streamer</code></br>
<code>cd /home/pi/mjpg-streamer</code></br>
<code>sudo apt-get install libjpeg8-dev</code></br>
<code>sudo apt-get install imagemagick</code></br>
<code>sudo apt-get install subversion</code></br>
<code>sudo svn co https://svn.code.sf.net/p/mjpg-streamer/code/mjpg-streamer/ .</code></br>
<code>sudo make</code></br>
<code>sudo mkdir /home/pi/stream</code></br>
<code>sudo chmod a+rw /home/pi/stream</code></br>
<code>sudo raspistill -w 640 -h 480 -q 5 -o /home/pi/stream/pic.jpg -tl 100 -t 9999999 -th 0:0:0 -n &</code></br>
<code>export LD_LIBRARY_PATH=/home/pi/mjpg-streamer/</code></br>
<code>mjpg-streamer/mjpg_streamer -i "input_file.so -f /home/pi/stream -n pic.jpg" -o "output_http.so -p 9000 -w /home/pi/mjpg-streamer/www" &</code></br>







# RTSP Server
#### 리눅스에서 카메라 입력을 받기위한 표준 인터페이스
<li>RTP/UDP unicast</li>
<li>RTP/UDP multicast</li>
<li>RTP/TCP</li>
<li>RTP/RTSP/HTTP</li>

## Usage 1.
### VLC
<code>$ sudo raspi-config </code></br>
"Enable Camera"</br>
<code>$ sudo apt-get update </code></br>
<code>$ sudo apt-get upgrade </code></br>
<code> sudo apt-get install vlc </code></br>
<code> sudo raspivid -o - -t 0 -n | cvlc -vvv stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264 </code></br>
<code> rtsp://IP:8554/ </code></br>


## Usage 2.
### V4L2 
#### Feature:
V4L2를 설치 후 활성화 시에 사용자 프로그램이 커널을 통해 I/O요청을 확인하고 장치 드라이버로 전송이 이루어지는 것이 가능해진다. 
사용자 프로그램이 커널을 통해 시스템 하드웨어에 접근 할 수 있도록 “dev” 디렉토리 내에 “video*"라는 장치 파일이 생성이 이루어진다. 
사용자는 이러한 “/dev/video”을 통해 자료를 읽거나 기타 장치로 자료를 전송이 가능해진다.

#### Session config:
v4l2rtspserver / dev / video0 : RTP 비디오 캡처 기능이있는 하나의 RTSP 세션 V4L2 장치 / dev / video0

<code>$ sudo raspi-config </code></br>
"Enable Camera"</br>
<code>$ sudo apt-get update </code></br>
<code>$ sudo apt-get upgrade </code></br>
<code>$ sudo apt-get install liblivemedia-dev libv4l-dev cmake libasound2-dev </code></br>
<code>$ sudo apt-get install v4l-utils </code></br>
<code>$ sudo modprobe bcm2835-v4l2 </code></br>
<code>$ sudo git clone https://github.com/mpromonet/h264_v4l2_rtspserver.git </code></br>
<code>$ cd h264_v4l2_rtspserver </code></br>
<code>$ sudo cmake . </code></br>
<code>$ sudo make </code></br>
<code>$  sudo ./h264_v4l2_rtspserver -F 25 -W 1280 -H 720 -P 8555 /dev/video0 & </code></br>

공식 V4L2 드라이버 bcm2835-v4l2
* 주의 : <code>$ sudo modprobe bcm2835-v4l2 </code>가 안될 시 장치 인식이 제대로 안되고 있다는 소리. 재부팅 시도.

#### Reboot 후 사용법:
<code>$ sudo modprobe bcm2835-v4l2 </code></br>
<code>$ cd h264_v4l2_rtspserver </code></br>
<code>$ sudo cmake . </code></br>
<code>$ sudo make </code></br>
<code>$  sudo ./h264_v4l2_rtspserver -F 25 -W 1280 -H 720 -P 8555 /dev/video0 & </code></br>
