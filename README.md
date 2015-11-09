# MP3CutAd
自动去掉MP3有声读物里面反复出现的片头、片尾、广告。

## 使用方法
下载安装（http://pan.baidu.com/s/1pJ3VmVx），或者：

1. 下载代码，用VS打开，会自动安装一些依赖。
2. 下载ffmpeg。复制里面的ffmpeg.exe和ffplay.exe到本项目的ffmpeg目录下。
3. 运行。

## 原理
找到**重复出现**的广告，然后去掉。

具体步骤如下：

1. 使用ffmpeg把MP3文件转成wav格式。（平均3~5秒一个文件）
2. 对wav文件做FFT。（大约2.5秒一个文件）
3. 对FFT的结果做LSH。（大约2.5秒一个文件）
4. 两两对比，找到相似的片段。（大约0.35秒对比一组）

运行时间根据一套有50个文件的有声读物实测得到，每个文件包含20分钟的录音，测试CPU为i5。
总时长为：4*50 + 2.5*50 + 2.5*50 + (1+2+...+49)*0.35 = 15分钟。


## TODO
* 考虑直接对MP3做fft，或许能快点。
* 目前是两两对比，找重复部分。考虑修改算法，归纳多处出现的广告，优化边界的识别。
* FFT+cos距离这种土办法是不是有高大上的替代方法？
* 边界判断是不是有高大上的替代方法？
* 新生成的MP3文件，加上原文件的标题、艺术家、专辑等信息。
* 没发现广告的文件，直接复制原文件过去。
* 各种重构，各种把参数提到一个地方。