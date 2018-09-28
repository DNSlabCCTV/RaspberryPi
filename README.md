# raspberryPi
<img src="/RPI_Camera.png" width="40%" height="40%"></br>
<code>$ sudo apt-get update </code>
<code>$ sudo apt-get upgrade </code>
<code>$ sudo apt-get install liblivemedia-dev libv4l-dev cmake libasound2-dev </code>
<code>$ sudo apt-get install v4l-utils </code>
<code>$ sudo modprobe bcm2835-v4l2 </code>
<code>$ sudo git clone https://github.com/mpromonet/h264_v4l2_rtspserver.git </code>
<code>$ cd h264_v4l2_rtspserver </code>
<code>$ sudo cmake . </code>
<code>$ sudo make </code>
<code>$  sudo ./h264_v4l2_rtspserver -F 25 -W 1280 -H 720 -P 8555 /dev/video0 & </code>
