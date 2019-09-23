##三体音视频SDK发版说明
###2.3.0版本
该版本于2019年8月19日发布。
###新增功能

####伴奏功能，相关接口以及回调
```
/**
 * 调节伴奏本地播放音量。
 *
 * @param volume 伴奏音量范围为0~100。默认50为原始文件音量。
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int adjustAudioMixingPlayoutVolume(int volume);
```

```
/**
 * 调节伴奏远端播放音量。
 *
 * @param volume 伴奏音量范围为0~100。默认50为原始文件音量。
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int adjustAudioMixingPublishVolume(int volume);
```

####外部音频源功能，相关接口以及回调
```
/**
 * 该方法设置是否使用外部音频源。
 *
 * @param enable     是否使用外部音频源。true使用，false不使用
 * @param sampleRate 外部音频源的采样率
 * @param channels   外部音频源的通道数，支持的参数为单声道(1)，双声道(2)
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int setExternalAudioSource(boolean enable, int sampleRate, int channels);
```

```
/**
 * 推送外部音频帧。
 *
 * @param data 外部音频数据。
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int pushExternalAudioFrame(byte[] data);
```

####摄像头功能，相关接口以及回调

```
/**
 * 检测设备是否支持摄像头缩放功能。
 *
 * @return true：设备支持相机缩放功能，false：设备不支持相机缩放功能
 */
public abstract boolean isCameraZoomSupported();
```

```
/**
 * 检测设备是否支持闪光灯常开。<br/>
 * 一般情况下，App 默认开启前置摄像头，因此如果你的前置摄像头不支持闪光灯常开，<br/>
 * 直接使用该方法会返回 false。如果需要检查后置摄像头是否支持闪光灯常开，需要先使用 switchCamera 切换摄像头，再使用该方法。<br/>
 *
 * @return true：设备支持闪光灯常开，false：设备不支持闪光灯常开
 */
public abstract boolean isCameraTorchSupported();
```

```
/**
 * 检测设备是否支持手动对焦功能。
 *
 * @return true：设备支持手动对焦功能，false：设备不支持手动对焦功能
 */
public abstract boolean isCameraFocusSupported();
```

```
/**
 * 检测设备是否支持手动曝光功能。
 *
 * @return true：设置支持手动曝光功能，false：设备不支持手动曝光功能
 */
public abstract boolean isCameraExposurePositionSupported();
```

```
/**
 * 检测设备是否支持人脸对焦功能。
 *
 * @return true：设备支持人脸对焦功能，false：设备不支持人脸对焦功能
 */
public abstract boolean isCameraAutoFocusFaceModeSupported();
```

```
/**
 * 设置摄像头缩放比例。
 *
 * @param factor 相机缩放比例，有效范围从 1.0 到最大缩放
 * @return true代表方法调用成功，false代表失败。
 */
public abstract boolean setCameraZoomFactor(int factor);
```

```
/**
 * 获取摄像头支持最大缩放比例。
 *
 * @return 该相机支持的最大缩放比例。
 */
public abstract int getCameraMaxZoomFactor();

```

```
/**
 * 设置是否打开闪光灯。
 *
 * @return true：打开，false：关闭
 */
public abstract boolean setCameraTorchOn(boolean isOpen);
```
####本地音频录音功能，相关接口以及回调

```
/**
 * 开始客户端录音
 *
 * @param filePath 录音文件的本地保存路径: xxx/.../xxx.aac
 * @param quality  录音质量，类型如下：<br/>
 *                 {@link Constants#TTT_AUDIO_RECORDING_QUALITY_LOW} 低音质。采样率为 48 kHz，码率 16 kpbs，录制 10 分钟的文件大小为 1.2 M 左右。<br/>
 *                 {@link Constants#TTT_AUDIO_RECORDING_QUALITY_MEDIUM} 中音质。采样率为 48 kHz，码率 32 kpbs，录制 10 分钟的文件大小为 2 M 左右。<br/>
 *                 {@link Constants#TTT_AUDIO_RECORDING_QUALITY_HIGH} 高音质。采样率为 48 kHz，码率 64 kpbs，录制 10 分钟的文件大小为 3.75 M 左右。<br/>
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int startAudioRecording(String filePath, int quality);
```

```
/**
 * 停止客户端录音
 *
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int stopAudioRecording();
```

```
/**
 * 本地音频录音完成通知。
 */
void onAudioRecordFinish();
```

####其他功能，相关接口以及回调
```
/**
 * 设置耳返音量，在打开耳返的情况下有效。
 *
 * @param volume 设置耳返音量，取值范围在 [0,100] 默认值为 100。
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int setAudioEarBackVolume(int volume);
```

```
/**
 * 获取网络连接状态
 *
 * @return 返回当前网络连接状态，类型如下：
 * {@link Constants#TTT_CS_DISCONNECTED} 未加入房间,加入房间失败后，或者离开房间之后。<br/>
 * {@link Constants#TTT_CS_CONNECTING} 加入房间正在建立网络连接。<br/>
 * {@link Constants#TTT_CS_CONNECTED} 网络连接建立成功。<br/>
 * {@link Constants#TTT_CS_RECONNECTING} 网络连接重连中。<br/>
 * {@link Constants#TTT_CS_FAILED} 网络连接失败。<br/>
 */
public abstract int getConnectionState();
```

```
/**
 * 网络连接状态发生改变。
 *
 * @param status 当前网络连接状态
 */
void onConnectionChangedToState(int status);
```

```
/**
 * 获取当前摄像头的ID，类型如下:<br/>
 * {@link Constants#TTT_CAMERA_FRONT} 代表前置摄像头<br/>
 * {@link Constants#TTT_CAMERA_BACK} 代表后置摄像头<br/>
 * {@link Constants#TTT_CAMERA_EXTERNAL} 代表外置摄像头<br/>
 *
 * @return 当前摄像头的ID。
 */
public abstract int getCameraFace();
```

```
/**
 * 设置默认订阅的视频流类型。
 *
 * @param streamType 设置视频流大小。视频流类型如下：<br/>
 *                   {@link Constants#VIDEO_STEAM_TYPE_BIG} 视频大流，即高分辨率、高码率视频流。<br/>
 *                   {@link Constants#VIDEO_STEAM_TYPE_SMALL} 视频小流，即低分辨率、低码率视频流。<br/>
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int setRemoteDefaultVideoStreamType(int streamType);
```

#-------------------------------------------

###2.4.0版本
该版本于2019年09月20日发布。
###新增功能

####音频自采集功能，相关接口以及回调
```
/**
 * 是否启用本地和远端音频混音后的裸数据上报
 *
 * @param enabled true代表启用上报，false代表禁用上报
 */
public abstract void enableMixAudioDataReport(boolean enabled);
```

```
/**
 * 设置本地音频裸数据的采样率，声道数和采样点数
 *
 * @param sampleRate     采样率，可设置为 8000，16000，32000，44100 或 48000
 * @param channel        声道数，最多支持两个声道
 * @param samplesPerCall 采样点数
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int setRecordingAudioFrameParameters(int sampleRate, int channel, int samplesPerCall);
```

```
/**
 * 设置远端音频裸数据的采样率，声道数和采样点数
 *
 * @param sampleRate     采样率，可设置为 8000，16000，32000，44100 或 48000
 * @param channel        声道数，最多支持两个声道
 * @param samplesPerCall 采样点数
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int setPlaybackAudioFrameParameters(int sampleRate, int channel, int samplesPerCall);
```

```
/**
 * 设置本地和远端音频混音裸数据的采样率，声道数和采样点数
 *
 * @param sampleRate     采样率，可设置为 8000，16000，32000，44100 或 48000
 * @param channel        声道数，最多支持两个声道
 * @param samplesPerCall 采样点数
 * @return 0代表方法调用成功，其他代表失败。see {@link LocalSDKConstants#FUNCTION_SUCCESS}
 */
public abstract int setMixedAudioFrameParameters(int sampleRate, int channel, int samplesPerCall);
```

```
/**
 * 获取录制和播放语音混音后的数据。
 *
 * @param data       PCM数据
 * @param size       PCM数据长度
 * @param sampleRate 采样率
 * @param channels   声道数
 */
byte[] onMixedAudioFrame(byte[] data, int size, int sampleRate, int channels);
```

### API变更
1.以下回调接口，会在参数列表末尾添加 **elapsed** 参数，表示当前回调自加入房间起，到触发该回调所用的时间。<br/>
onJoinChannelSuccess<br/>
onUserJoined<br/>
onFirstLocalVideoFrame<br/>
onFirstRemoteVideoDecoded<br/>
onFirstRemoteVideoFrame<br/>
onFirstRemoteVideoDecoded<br/>
onFirstRemoteVideoFrame<br/>

2.以下音频裸数据回调的返回值从 **void** 变更为 **byte[]**，支持对裸数据进行二次处理，将处理完的数据返回给sdk，sdk再进行后续处理。<br/>
onLocalAudioDataReport<br/>
onRemoteAudioDataReport<br/>

3.**ScreenRecordConfig** 类中字段 **mRecordAudioBitRate** 设置音频码率的字段去掉。添加字段 **mRecordIFrameInterval** 设置视频关键帧间隔。
