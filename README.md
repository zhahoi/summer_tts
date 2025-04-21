# summer_tts
在ROS中使用SummerTTS进行语音合成。SummerTTS 是一个独立编译的语音合成程序(TTS)。可以本地运行不需要网络，而且没有额外的依赖，一键编译完成即可用于中文和英文的语音合成。



### 写在前面

创建本仓库的初衷是为了想在ROS中使用语音合成，播报目标检测的检测结果或者进行语音交互使用。但是在网上搜索一圈发现，基本上没有免费离线的TTS并且还需要注册和联网（说的就是你，科大讯飞）。本着能白嫖就白嫖的原则，便在github搜索一番，发现一个很棒的离线的TTS仓库[SummerTTS](https://github.com/huakunyang/SummerTTS)，还是用C++写的，看到这个仓库之后，真的是两眼放光，立马克隆下来研究一番。(**十分建议在使用本仓库之前，仔细观看原仓库SummerTTS使用说明**)。

自己下载、编译并运行测试脚本之后发现，该项目基本上满足了我的基本需求，可以选择中文或者英文的语音输出，并且处理速度相对算快，因此想将其转换成可以在ros中使用的代码。花费了约两三个小时的时间完成了该仓库。

**本仓库的代码几乎全部来自于[SummerTTS](https://github.com/huakunyang/SummerTTS)源仓库，只针对于main.cpp文件进行了修改，创建话题，使其可以在ros中使用。在这里再次感谢源仓库博主[huakunyang](https://github.com/huakunyang)的无私奉献。**

此外，本仓库的代码编写思路参考了以下的博客文章：[【ROS】科大讯飞TTS SDK 语音合成](https://zhuanlan.zhihu.com/p/695906352)，在这里也表示感谢。



### 测试环境

系统：ubuntu 20.04

ros环境：noetic



### 编译

本仓库的使用方法如下：

（1）先创建一个工作空间，将本仓库的代码拷贝到src文件夹下

```sh
$ mkdir -p summer_tts_ws/src
$ cd summer_tts_ws/src/
$ catkin_init_workspace
$ git clone https://github.com/zhahoi/summer_tts.git
```

（2）下载tts权重文件

因为SummerTTS是离线的tts模型，因此需要下载权重。源仓库文件提供了权重文件的下载链接，其百度云链接如下: https://pan.baidu.com/s/1rYhtznOYQH7m8g-xZ_2VVQ?pwd=2d5h 提取码: 2d5h  ，下载完成后，将权重放置到`summer_tts/models`的路径下。

（3）修改重要的文件路径

用编辑器打开`summer_tts/src`路径下的`summer_tts_node.cpp`文件，修改以下三个路径地址，将其改为实际项目的绝对路径：

```c++
char* modelPath="/home/hit/summer_tts_ws/src/summer_tts/models/single_speaker_fast.bin"; //加载tts模型权重
const char* audioPath="/home/hit/summer_tts_ws/src/summer_tts/audios/robot_audio.wav"; // 生成的wav文件保存路径
const char* playPath="play /home/hit/summer_tts_ws/src/summer_tts/audios/robot_audio.wav"; // 播放音频的脚本
```

注：为了能够让语音可以播放成功，需要提前安装一个SoX 工具包，以支持`play`播放。

```sh
$ sudo apt-get install sox
```

（4）编译整个工作空间

```sh
$ cd 到 summer_tts_ws文件夹
$ catkin_make  //编译
```



### 测试

- 开启第一个终端：

  ```sh
  $ roscore
  ```

- 开启第二个终端**（在工作空间根目录打开）**：

  ```sh
  $ source devel/setup.bash
  $ rosrun summer_tts summer_tts_node
  ```

  等待1-2秒你会听到一个女生播报"**语音合成模块启动**"，这就代表本仓库代码基本运行成功。

  

![输出1](https://github.com/zhahoi/summer_tts/blob/main/docs/%E8%BE%93%E5%87%BA1.png)

- 通过rostopic pub手动发布消息来让其播报(**新开启一个终端**)

  ```sh
  $ rostopic list  // 查看话题名
  $ rostopic pub /summer_tts_topic std_msgs/String "你好，世界"
  ```

  输入以上指令后，你会听到女声播报”**你好，世界**“。

  ![输出2](https://github.com/zhahoi/summer_tts/blob/main/docs/%E8%BE%93%E5%87%BA2.png)

![输出3](https://github.com/zhahoi/summer_tts/blob/main/docs/%E8%BE%93%E5%87%BA3.png)



以上已经基本实现通过发布“`/summer_tts_topic`”话题，来实现tts语音播报功能。



### 写在最后

创作不易，如果觉得这个仓库还可以的话，麻烦给一个star，这就是对我最大的鼓励。



### References

-[SummerTTS](https://github.com/huakunyang/SummerTTS)
