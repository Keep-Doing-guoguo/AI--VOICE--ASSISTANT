
# 1.AI 语音交互助手系统（实时 ASR + LLM + Web 前端）

### 1.1.技术栈： 

Python（FastAPI、WebSocket、DashScope、pyaudio）、JavaScript（MediaRecorder、Web Audio API）、HTML/CSS、SiliconFlow API、DeepSeek-V2.5、Threading、Queue、SSE、Docker

### 1.2.项目简介：

独立设计与开发一个支持实时语音识别、连续听写、多轮上下文理解及流式回答输出的智能语音助手系统。系统采用麦克风实时录音，通过 DashScope gummy-realtime-v1 进行语音识别（ASR），识别完成的语句自动送入大模型（DeepSeek-V2.5）进行推理，并通过 SSE/WebSocket 将生成内容逐字实时返回到页面。

### 1.3.核心功能：

	•	🎤 实时语音采集：支持浏览器麦克风录音、会议语音设备、虚拟声卡等多种音源输入。
	•	🧠 智能语义理解：在 ASR 识别到句子结束时自动触发 LLM 调用，支持多轮上下文记忆，保留近 10 条历史对话。
	•	⚡ 流式响应：使用 SSE/WebSocket 将 DeepSeek 返回结果逐字实时推送到前端，打造 ChatGPT 式语音助手交互体验。
	•	🧵 异步架构设计：采用线程 + 队列模型（Threading + Queue），实现 ASR 与 LLM 并行处理，提升实时响应效果。
	•	💻 Web 端 UI：自研前端页面，支持录音按钮控制、语音转文字展示、流式回答滚动输出、对话记录展示。
	•	🔌 API 封装：封装成 /v1/voice-chat HTTP API 和 /ws/voice-stream WebSocket 接口，同时兼容 OpenAI 格式。

### 1.4.技术亮点：

✔ 实现实时音频分帧采集与句末判断触发机制（is_sentence_end）
✔ 构建语音输入 → ASR → LLM → 流式回答 → 前端展示 的完整实时系统链路
✔ 使用 FastAPI + SSE + WebSocket 实现低延迟流式推送，支持并发
✔ 支持切换音频输入设备，可用于会议 AI 助手、面试助手、客服助手等场景
✔ 设计可扩展架构，LLM 可一键切换 DeepSeek、GPT、通义千问等模型

### 1.5.效果展示：

用户在网页中点击“开始录音” → 开始讲话 → 自动识别并触发 AI 回答 → 实时生成文字回答并输出到页面 → 支持持续对话不必重复点击录音。


本项目提供两个接口功能和一个控制台功能：

1. /v1/voice-chat HTTP 接口：支持上传音频文件进行语音识别和 LLM 回答，适合离线处理场景。

![](./v1/voice-chat.png)


2. /v1/voice-chat-stream HTTP 接口：支持上传音频文件进行语音识别和 LLM 流式回答，适合需要逐步获取回答的场景。

![](./v1/前端流失返回.png)

3. /ws/voice-stream WebSocket 接口：支持浏览器实时录音流式传输，适合在线实时交互场景。

这里指的是，当打开服务的时候，系统会根据你说的话来进行回答问题。



4. Web 控制台：提供录音按钮、文字展示区域、对话记录等交互功能。

这里指的是，在控制台进行录音，系统会根据你说的话来进行回答问题。



