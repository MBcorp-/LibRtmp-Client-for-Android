# Librtmp Client for Android
It is probably the smallest(~60KB) rtmp client for android. It calls librtmp functions over JNI interface.
With all cpu architectures(arm, arm7, arm8, x86, x86-64, mips) its size is getting about 300KB

It compiles librtmp library without ssl. 

In version 0.2, it supports FLV muxing and sending stream via RTMP. FLV muxing is based on this repo https://github.com/rainfly123/flvmuxer


#####To read streams, you can call below functions of **RtmpClient** from Java#####

For live streams add **" live=1"** at the end of the url when calling the **_open_** function

* *public native int open(String url, boolean isPublishMode);*
* *public native int read(byte[] data, int offset, int size);*
* *public native int write(byte[] data);*
* *public native int seek(int seekTime);*
* *public native int pause(int pause);*
* *public native int close();*

Don't forget calling the **_close_** function after you are done. If you don't, there will be memory leakage


#####To publish streams, you can call below functions of **RtmpMuxer** from Java#####
* *public native int open(String url);* : First, call this function with the url you plan to publish  
* *public native int writeVideo(byte[] data, int offset, int length, int timestamp);*: Write h264 nal units with this function
* *public native int writeAudio(byte[] data, int offset, int length, int timestamp);*: Write aac frames with this function
* *public native int close();*: Call this function to close the publishing.

To save flv file locally as well, you can use below functions
* *public native void file_open(String filename);* : call this function with full file path
* *public native void write_flv_header(boolean is_have_audio, boolean is_have_video);*: After opening file call this function
* *public native void file_close();*: Call this function to close the file. 

if any local file is opened, library will write the audio and video frames to local file as well. 

## Install ##

- Add dependency to your build gradle
```sh
dependencies {
    ...
    compile 'net.butterflytv.utils:rtmp-client:0.2.1'
    ...
}
```

- That's all. You can use RtmpClient class


<br/>
This project is developed for Butterfly TV <a href="http://www.butterflytv.net/"><img src="http://www.butterflytv.net/wp-content/uploads/2014/08/icon-butterflyTV-150x150.png" width="30"></a>

<a href="https://play.google.com/store/apps/details?id=com.butterfly">
  <img alt="Get it on Google Play" width="200px" src="https://play.google.com/intl/en_us/badges/images/generic/en-play-badge.png">
</a>
