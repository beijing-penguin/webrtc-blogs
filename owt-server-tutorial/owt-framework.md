
## MCU和SFU
OWT-Server架构时基于MCU和SFU架构基础形式开发的流媒体服务。SFU和MCU的区别（如下图）

<p align="center"><img width="100%" src="../img/5.png" /></p>

一、Mesh架构

即：每个端都与其它端互连。以上图最左侧为例，5个浏览器，二二建立p2p连接，每个浏览器与其它4个建立连接，总共需要10个连接。如果每条连接占用1m带宽，则每个端上行需要4m，下行带宽也要4m，总共带宽消耗20m。而且除了带宽问题，每个浏览器上还要有音视频“编码/解码”，cpu使用率也是问题，一般这种架构只能支持4-6人左右，不过优点也很明显，没有中心节点，实现很简单。

二、MCU (MultiPoint Control Unit)

每个浏览器仅与中心的MCU服务器连接，MCU服务器负责所有的视频编码、转码、解码、混合等复杂逻辑，每个浏览器只要1个连接，整个应用仅消耗5个连接，带宽占用(包括上行、下行）共10m，浏览器端的压力要小很多，可以支持更多的人同时音视频通讯，比较适合多人视频会议。但是MCU服务器的压力较大，需要较高的配置。

三、SFU(Selective Forwarding Unit)

中心节点只负责转发，不做太重的处理，服务器的压力会低很多，配置也不象MUC要求那么高。但是每个端需要建立一个连接用于上传自己的视频，同时还要有N-1个连接用于下载其它参与方的视频信息。所以总连接数为5*5，消耗的带宽也是最大的，如果每个连接1M带宽，总共需要25M带宽，它的典型场景是1对N的视频互动。


## OWT架构
`OWT-Server` 不仅支持SFU模式(owt安装完成后，可以SFU直接访问demo页面：`https://192.168.72.140:3004/?forward=true`)，同时也支持MCU视频混合模式（`https://192.168.72.140:3004`）。

 **Table 2-5. Distributed OWT server components**
Component Name|Deployment Number|Responsibility
--------|--------|--------
management-api|1 or many|The entrance of OWT service, keeping the configurations of all rooms, generating and verifying the tokens. Application can implement load balancing strategy across multiple management-api instances
cluster-manager|1 or many|The manager of all active workers in the cluster, checking their lives, scheduling workers with the specified purposes according to the configured policies. If one has been elected as master, it will provide service; others will be standby
portal|1 or many|The signaling server, handling service requests from Socket.IO clients
conference-agent|1 or many|This agent handles room controller logics
webrtc-agent|1 or many|This agent spawning webrtc accessing nodes which establish peer-connections with webrtc clients, receive media streams from and send media streams to webrtc clients
streaming-agent|0 or many|This agent spawning streaming accessing nodes which pull external streams from sources and push streams to rtmp/rtsp destinations
recording-agent|0 or many|This agent spawning recording nodes which record the specified audio/video streams to permanent storage facilities
audio-agent|1 or many|This agent spawning audio processing nodes which perform audio transcoding and mixing
video-agent|1 or many|This agent spawning video processing nodes which perform video transcoding and mixing
analytics-agent|0 or many|This agent spawning media analyzing nodes which perform media analytics
sip-agent|0 or many|This agent spawning sip processing nodes which handle sip connections
sip-portal|0 or 1|The portal for initializing rooms' sip settings and scheduling sip agents to serve for them
app|0 or 1|The sample web application for reference, users should use their own application server
management-console|0 or 1|The console for conference management