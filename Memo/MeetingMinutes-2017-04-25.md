## 七牛插件化SDK平台设计初稿：
## 设计背景：
目前联盟内各个厂商均有自己的SDK，各自有各自的优势，熊猫基于业务需求及联盟发展规划，重新设计插件化SDK平台方案，可以兼容各家SDK，博采众长，将联盟推流SDK打造为市面上最优秀、最全面、兼容性最高的推流SDK产品。

## 模块设计：
暂定将SDK拆分为采集、编码、传输、连麦等几个模块，SDK支持配置列表，在APP第一次启动时，可以远程获取模块配置，支持插件化升级方案（IOS由于Appstore审核机制暂不考虑）。具体模块如下：
- 采集模块：
七牛提供。

- 传输模块：
分为RTMP和私有协议（UDP）,七牛RTMP作为标准推流协议，同时兼容星域/网宿/百度等厂家的私有UDP传输模块。预计5月份会先和星域对接，并以该接口为传输层模块接口规范。届时推流SDK策略为：向熊猫服务端获取推流URL—能力协商，判断收流厂商是否支持私有协议（UDP）—若支持，便调用该厂商UDP模块—若UDP不通，则改为标准RTMP推流。

- 连麦：
设计连麦能力协商API，客户可根据用户等级体系、特定业务场景等业务需求，决定具体使用哪种方案。

- 编码：
熊猫会先考察网宿H.265方案，若可行，便让网宿开放源代码，其他厂商提修改意见，一起打造为公用H.265方案，时间规划为年底。

以上插件化平台打造完毕后，APP第一次启动时做模块加载，不会在使用过程中动态更换。大体流程是：APP启动——获取配置列表（七牛提供配置列表service）——本地检查（获取模块、版本升级）——返回ready——APP调取使用。
