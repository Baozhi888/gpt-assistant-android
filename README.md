# GPT Assistant

---

## 简介

GPT Assistant 是一个基于ChatGPT的安卓端语音助手，允许用户通过手机音量键从任意界面唤起并直接进行语音交流，用最快捷的方式询问并获取回复

### 项目特性

- 支持用户预设**问题模板**，支持**连续对话**，支持`gpt-3.5-turbo`、`gpt-4`等模型
- **支持联网**，允许GPT获取在线网页
- 通过无障碍功能捕获音量键事件，实现在**任意界面唤起**
- 支持从**全局上下文菜单**（选中文本后弹出的系统菜单）中直接唤起
- 支持通过状态栏**快捷按钮**唤起
- 支持对**Markdown**进行渲染
- 使用华为或百度语音API进行**语音输入**
- 调用系统TTS引擎**输出语音**

### 国内使用说明

本软件通过OpenAI API获取回复，在国内使用时可以用第三方转发服务，如[Chatanywhere](https://github.com/chatanywhere/GPT_API_free)，其目前提供免费和付费服务，具体使用方法见[下述说明](#使用方法)

> 注：Chatanywhere注册需要GitHub账号，因此注册时需要能够登录GitHub的网络环境

### 费用说明

本软件不会收取任何费用，用户能够免费使用各项功能，但如果有特殊需求，使用的下述第三方服务**可能**会产生费用:

1. ChatGPT调用费用

	- 以Chatanywhere为例，目前其**免费服务**限制对`gpt-3.5-turbo`模型的调用频率不超过**60请求/小时/IP&Key**，足够个人使用，若需要更高的调用频率或`gpt-4`模型，可以选择付费服务

2. 百度语音识别接口费用

	- 目前华为HMS提供免费的语音识别接口，因此程序内置了作者的API Key以供直接使用，如无特殊情况该API将在华为免费期间一直可用

	- 程序也提供了对百度接口的调用以供有需要的情况下使用，目前百度短语音识别为新用户提供**15万次 & 180天免费额度**，额度外收取￥0.0034/次的调用费用

---

## 效果展示

**一、基础使用：仅用音量键就可以操控**

1. 长按音量下键唤出界面

2. 按住音量键不放，开始语音输入

3. 松开后再次短按，发送问题

4. 接收回复的同时可以自动通过语音进行播报

<div align="center">
	<img src="readme_img/usage.gif" height="400px">
</div>

**二、用状态栏快捷键也可触发**

下拉状态栏，点击“GPT”按钮，即可唤出界面，键盘会自动弹出，可以手动输入问题

<div align="center">
	<img src="readme_img/tile_btn.gif" height="400px">
</div>

**三、从全局上下文菜单唤起**

在选中文本后弹出的系统菜单中，点击GPTAssistant选项，即可直接唤起应用并将选中文本添加到输入框

<div align="center">
	<img src="readme_img/context_menu.gif" height="400px">
</div>

**四、支持连续对话**

激活上方的对话图标，即可保留当前会话，进行连续对话

<div align="center">
	<img src="readme_img/multi_chat.gif" height="400px">
</div>

**五、支持GPT联网**

本程序实现了OpenAI的Function接口，允许GPT发起联网请求，程序会向GPT自动返回所需的网页数据，使GPT具有联网能力（需先在设置中开启联网选项）

<div align="center">
	<img src="readme_img/web_time.png" height="120px">
	<img src="readme_img/web_weather.png" height="120px">
</div>
<div align="center">
	<img src="readme_img/web_zhihu.png" height="200px">
	<img src="readme_img/web_exchange.png" height="200px">
</div>

> 注1：上图均为使用`gpt-3.5-turbo-0613`模型的测试结果，建议在提问前加入“百度搜索”、“在线获取”、“从xxx获取”等字样引导GPT，以获得更好的联网效果

> 注2：由于需要将网页内容发送给GPT，联网时会产生大量Token消耗，`gpt-4`模型请谨慎使用

---

## 使用方法

### 1. 下载安装

直接下载最新发行版中的apk文件，安装即可

### 2. 配置 OpenAI

程序使用的是OpenAI API，需要用户在设置中填入自己的API_KEY，可以选择使用官方服务或第三方转发服务

- **使用Chatanywhere转发服务**（国内推荐）

	Chatanywhere提供了免费和付费的OpenAI API转发服务，目前免费服务限制60请求/小时/IP&Key调用频率，付费服务则无限制，可以在国内直接访问，用户可以参照其[项目主页](https://github.com/chatanywhere/GPT_API_free)获取地址和KEY填入设置中

- **使用官方服务**

	在OpenAI官网注册账号并获取API_KEY，在设置中填写网址`https://api.openai.com/`和API_KEY

### 3. 配置百度语音识别 (可选)

> 注：程序默认使用的是华为语音识别接口，如无特殊情况，不需要进行此步骤

用户可以参照[百度语音识别官方文档](https://cloud.baidu.com/doc/SPEECH/s/qknh9i8ed)注册并创建应用，然后获取AppID、API Key和Secret Key填入设置中

若设置项的“启用长语音”选项关闭，则使用的是百度短语音识别接口，若开启，则使用的是实时语音识别接口，需要用户根据需求在创建应用时勾选对应的服务

此外，在创建应用时，需要将“语音包名”设置为“Android”，并填入本软件包名`com.skythinker.gptassistant`

![设置语音包名](readme_img/asr_set_package.jpg)

### 4. 开始使用

1. 根据软件提示开启无障碍服务，并允许软件在后台运行

2. 查看设置中是否存在“后台弹出界面”权限，如有该权限则允许，如无则忽略

	> 若发现长按音量下键后手机震动一下但没有弹出界面，大概率是因为缺少该权限

3. 开始正常使用，可参照[效果展示](#效果展示)中的操作步骤

---

## Q&A

**Q: 长按音量下键只是在调节音量，并没有其他任何现象？**

A: 请在设置中开启本软件的无障碍服务（重启手机后可能需要重新开启，建议设置为无障碍快捷方式）

**Q: 长按音量下键后，手机震动了一下，但没有弹出界面？**

A: 请在设置中允许程序“后台弹出界面”权限

**Q: 隔一段时间不用就无法使用音量键唤起了？**

A: 请在设置中允许程序在后台运行

**Q: 语音播报没声音 / 不好听？**

A: 软件调用的是系统自带TTS(Text To Speech)服务，可以通过软件设置项“打开系统语音设置”进入系统设置界面，选择合适的语音引擎；若对系统自带引擎不满意也可以自行安装讯飞等第三方TTS引擎

**Q: 华为和百度语音识别效果有什么差别？**

A: 经测试，所使用的华为接口（实时语音识别）识别准确度较高，尤其是在中英混说的场景下，但其断句能力则不如百度，仅适合单句识别

**Q: GPT返回的Markdown中表格和图片无法正常显示？**
A: 所使用的Markdown渲染器无法在测试中产生稳定的结果，因此暂不支持表格和图片

---

## 主要功能更新日志

- **2023.09.10** 发布第一个版本，支持基础对话、百度语音输入、TTS输出、Markdown渲染等功能
- **2023.09.13** 支持连续对话、GPT-4、百度长语音识别，上下文菜单唤起
- **2023.10.06** 添加华为HMS语音识别
- **2023.11.06** 添加联网功能

---

## 测试环境

已测试的机型：

| 机型 | 系统版本 | Android 版本 | 本程序版本 |
| :--: | :-----: | :----------: | :-------: |
| 荣耀 7C | EMUI 8.0.0 | Android 8 | 1.6.0 |
| 荣耀 20 | HarmonyOS 3.0.0 | Android 10 | 1.6.0 |
| 华为 Mate 30 | HarmonyOS 3.0.0 | Android 12 | 1.4.0 |
| 荣耀 Magic 4 | MagicOS 7.0 | Android 13 | 1.2.0 |
| 红米 K20 Pro | MIUI 12.5.6 | Android 11 | 1.5.0 |
| 红米 K60 Pro | MIUI 14.0.23 | Android 13 | 1.6.0 |
| Pixel 2 (模拟器) | Android 12 | Android 12 | 1.2.0 |

---

## 改进&贡献

如果你有改进建议或希望参与贡献，欢迎提交Issue或Pull Request

---

## 隐私说明

本程序不会以任何方式收集用户的个人信息，语音输入会直接发送给华为或百度API，提问会直接发送给OpenAI API，不会经过任何中间服务器

---

## 引用的开源项目

- [Markwon](https://github.com/noties/Markwon): Android上的Markdown渲染器
- [chatgpt-java](https://github.com/Grt1228/chatgpt-java): OpenAI API的Java封装
