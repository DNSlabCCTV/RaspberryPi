# raspberryPi
<img src="/RPI_Camera.png" width="40%" height="40%"></br>

## Usage 1.
<code> sudo apt-get install vlc </code></br>
<code> sudo raspivid -o - -t 0 -n | cvlc -vvv stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264 </code></br>
<code> rtsp://IP:8554/ </code></br>


## Usage 2.
### V4L2 
#### 리눅스에서 카메라 입력을 받기위한 표준 인터페이스
#### Feature:
V4L2를 설치 후 활성화 시에 사용자 프로그램이 커널을 통해 I/O요청을 확인하고 장치 드라이버로 전송이 이루어지는 것이 가능해진다. 
사용자 프로그램이 커널을 통해 시스템 하드웨어에 접근 할 수 있도록 “dev” 디렉토리 내에 “video*"라는 장치 파일이 생성이 이루어진다. 
사용자는 이러한 “/dev/video”을 통해 자료를 읽거나 기타 장치로 자료를 전송이 가능해진다.

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

* 주의 : <code>$ sudo modprobe bcm2835-v4l2 </code>가 안될 시 장치 인식이 제대로 안되고 있다는 소리. 재부팅 시도.
