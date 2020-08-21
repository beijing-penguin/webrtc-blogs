```
build 编译所需的依赖库
    |---expat
    |---ffmpeg
    |---libnice
    |---libsrtp
    |---openssl
    |---re
    |---usrsctp
    |---zlib
cert
dist 编译生成的服务，集群配置
doc 说明文档
docker
node_modules
scripts  脚本执行入口
         |----installDepsUnattended.sh  安装依赖
         |----build.sh 编译
         |----pack.js 打包
         |----installCommonDeps.sh 安装模块，包含webrtc
source
      |----agent
             |----addons
             |----analytics
             |----audio  音频的处理，转码，混音
             |----conference 房间的控制逻辑
             |----plugins
             |----recording 录制媒体
             |----sip  sip接入
             |----streamig 拉取流媒体转换成rtmp或rtsp
             |----video 视频的处理，转码，混音
             |----webrtc webrtc接入
                     
      |----cluster_manager 控制集群的works，调度works
      |----common
      |----core
      |----data_access
      |----management_api
      |----management_console
      |----portal 信令服务器，处理io请求
              |----socketIOServer.js  信令监听
              |----v10Client.js    信令监听
      |----sip_portal
test
third_party
    |----licode
            |----erizo  c++实现的webrtc栈
            |----erizoAPI  对erizo的封装，实现js调用c++
            |----erizo_controller 客户端和服务器的接口模块
    |----mediasdk
    |----openh264
    |----quic-lib
    |----svc-hevc
    |----webrtc
           |----src
                 |----tools-woogeen 编译脚本，只用了部分模块
                 |----install.sh 下载依赖模块
                 |----build.sh  说明了用到的模块，编译成libwebrtc.a
                 |----third_party  用到的模块并不多
                            |----libvpx
                            |----libyuv
                            |----opus
                            |----protobuf
                            |----yasm
```