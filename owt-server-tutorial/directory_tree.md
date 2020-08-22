```
├── build 编译所需的依赖库
│   └── libdeps
│       ├── build
│       ├── expat-2.2.6
│       ├── ffmpeg-4.1.3
│       ├── libnice-0.1.4
│       ├── openssl-1.1.1g
│       ├── re
│       ├── usrsctp
│       ├── zlib-1.2.11
├── cert 证书
│   ├── certificate.pfx
│   ├── cert.pem
│   └── key.pem
├── dist 打包生成的可运行目录
│   ├── analytics_agent 流媒体分析
│   ├── apps 浏览器前端展示页面
│   ├── audio_agent 音频处理
│   ├── bin 停止、启动、初始化脚本
│   ├── cluster_manager 集群管理服务
│   ├── conference_agent 会议管理服务
│   ├── logs 日志
│   ├── management_api 外网管理API可访问接口
│   ├── management_console 外网管理控制台页面
│   ├── portal 长连接websocket服务
│   ├── recording_agent 视频录制
│   ├── sip_agent 信令处理
│   ├── sip_portal 信令
│   ├── streaming_agent 流处理
│   ├── video_agent 视频编解码
│   └── webrtc_agent 长连接webrtc网关
├── doc 说明文档
├── docker
├── node_modules
├── scripts 脚本
├── source 源码代码目录
│   ├── agent 类似微服务模块目录
│   ├── cluster_manager 集群管理者
│   ├── common 公共模块，rpc请求工具，rabbitmq连接工具，日志打印工具等
│   ├── core 核心C/C++模块
│   ├── data_access 数据模块
│   ├── management_api 外网管理API可访问接口
│   ├── management_console 外网管理控制台页面
│   ├── portal 长连接websocket服务
│   └── sip_portal 信令SIP服务
├── test 测试程序
└── third_party 第三方依赖模块
    ├── licode
    ├── mediasdk
    ├── openh264
    ├── quic-lib
    ├── SVT-HEVC
    ├── webrtc 编译后的webrtclib.a和一些.h头文件
    └── webrtc-m79 谷歌webrtc客户端源码
```
