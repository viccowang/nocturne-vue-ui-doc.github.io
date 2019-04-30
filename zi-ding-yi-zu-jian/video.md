## ZHX Video Component

---

#### 描述

该组件可以实现在框架中嵌入视频流,直播流或者音频流等多媒体内容.支持包括MP4文件播放,HLS直播,RTMP直播等多种协议.
组件使用了开源的```VideoJS```视频播放模块作为基础组件. 在此基础上实现了```Vue```框架的扩展.可以全局或在模块中单独引入.

#### 起步

**全局引入**
```js
// main.js
import VueVideoPlayer from '@/components/videoPlayer'
```

**局部引入**
```js
// Foo Components
import { videoPlayer } from '@/components/videoPlayer'
// rtmp 直播流需要使用flash
require('videojs-flash')
// HLS 直播流需要使用videojs-contrib-hls plugin
require('videojs-contrib-hls')

export default {
    ...
    components: { videoPlayer }
    ...
}
```

**模板定义**
```html
<video-player :options="videoOpts" />
```



#### Video Player 配置项
> 这里的事件除```@ready```事件外,都映射自```VideoJS```组件中的事件

##### 常用配置(更多配置请移步[```VideoJS```官网](http://docs.videojs.com/index.html)查看)
| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| autoPlay | 是否自动播放 | Boolean | true/false | true |
| controls | 是否启用播放控制 | Boolean | true/false | true |
| controlBar | 播放控制选项(请参考[```VideoJS```官网](http://docs.videojs.com/index.html)) | Object | - | - |
| preload | 是否在播放前进行预载入 | String| auto/none/metadata | auto |
| fluid | 播放器大小是否根据父容器进行自适应 | Boolean | true/false | true |
| muted | 是否启用静音 | Boolean | true/false | false |
| playbackRates | 回放速度级别配置,用户可以选择几倍速度进行播放 | Array | [0.5, 1.0, 1.5, 3] | 1.0 |
| sources | 播放源配置(请参考[```VideoJS```官网](http://docs.videojs.com/index.html)) | Array | - | - |
| poster | 播放器默认封面 | String | - | - |

##### 事件
| 名称 | 说明 | 回调函数参数 |
| :--- | :--- | :--- |
| loadeddata | 内容读取完毕 | VideoJS实例 |
| canplay | 可以播放 |VideoJS实例 |
| play | 开始播放 |VideoJS实例 |
| pasue | 暂停播放 |VideoJS实例 |
| waiting | 等待中 |VideoJS实例 |
| playing | 正在播放 |VideoJS实例 |
| ended | 播放完毕 |VideoJS实例 |
| error | 播放失败 |VideoJS实例 |
|ready | VideoJS 组件完成初始化后触发 | Video Player 实例 |

#### 常见MP4 / HLS / RTMP的简单配置demo

**通用的模板配置**
```html
// Foo Template
<video-player
    :options="playerOpts"
    @play="onPlayerPlay($event)"
    @pause="onPlayerPause($event)"
    @ended="onPlayerEnded($event)"
    @ready="playerReady($event)"
  />
```

**播放mp4**

```js
// Foo Component
export default {
    ...
    data () {
        return {
            playerOpts: {
                autoplay: false,
                muted: true,
                playbackRates: [0.7, 1.0, 1.5, 2.0],
                sources: [{
                  type: 'video/mp4',
                  src: '//vjs.zencdn.net/v/oceans.mp4'
                }],
                poster: '//vjs.zencdn.net/v/oceans.png'
            }
        }
    },
    ...
}
```

**播放HLS**

```js
// Foo Component
// HLS 直播流需要使用videojs-contrib-hls plugin
require('videojs-contrib-hls')

export default {
    ...
    data () {
        return {
            playerOpts: {
                muted: true,
                sources: [{
                  withCredentials: false,
                  type: 'application/x-mpegURL',
                  src: 'http://playertest.longtailvideo.com/adaptive/bipbop/gear4/prog_index.m3u8'
                }],
                poster: '//vjs.zencdn.net/v/oceans.png'
            }
        }
    },
    ...
}
```

**播放RTMP**

> **[info] 并不建议使用RTMP ** 
>
> 我们并不建议使用RTMP流进行播放, 在未来的技术演进上,```flash```播放必然会被淘汰掉.取而代之的是HLS等支持HTML5格式的技术.因此,在条件允许的情况下, 尽可能使用其他解决方案.

```js
// Foo Component
// rtmp直播流需要使用flash
require('videojs-flash')

export default {
    ...
    data () {
        return {
            playerOpts: {
                autoplay: false,
                muted: true,
                techOrder: ['flash'], // rtmp 必须指定techOrder 为 flash
                sources: [{
                  type: 'rtmp/mp4',
                  src: 'rtmp://live.hkstv.hk.lxdns.com/live/hks'
                }],
                poster: '//vjs.zencdn.net/v/oceans.png'
            }
        }
    },
    ...
}
```