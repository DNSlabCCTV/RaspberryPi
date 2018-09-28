# raspberryPi
<img src="/RPI_Camera.png" width="40%" height="40%"></br>

## Usage 1.
<code> sudo apt-get install vlc </code></br>
<code> sudo raspivid -o - -t 0 -n | cvlc -vvv stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/}' :demux=h264 </code></br>
<code> rtsp://192.168.0.46:8554/ </code></br>


## Usage 2.
### V4L2
#### Feature:


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
