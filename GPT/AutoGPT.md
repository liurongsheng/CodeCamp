# AutoGPT

AutoGPT 是一个实验性开源应用程序，它利用 OpenAI 的 GPT-4 语言模型来创建完全自主和可定制的 AI 代理。它于 2023 年 3 月 30 日由 Toran Bruce Richards 发行

与其他 AI 工具相比，AutoGPT 是独一无二的，因为它独立运行，这意味着你不再需要操纵模型来满足你的需求。相反，你只需要写下你的目标，然后 AI 会为你完成剩下的工作

因此，AutoGPT 从根本上改变了 AI 与人类之间的交互方式，人类不再需要发挥积极作用，同时仍然保持与 ChatGPT 等其他 AI 应用程序相同或更好的结果质量

## AutoGPT 如何工作

AutoGPT 基于自主 AI 机制工作，其中 AI 系统创建不同的 AI 代理来满足特定任务，其中包括：

任务创建代理： 当你在 AutoGPT 上输入目标时，第一个与任务创建代理交互的 AI 代理。根据你的目标，它将创建一个任务列表以及实现这些目标的步骤，并将其发送给优先级代理
任务优先级代理： 收到任务列表后，优先级 AI 代理会确保顺序正确且符合逻辑，然后再将其发送给执行代理
任务执行代理： 完成优先级排序后，执行代理将一个接一个地完成任务。这涉及利用 GPT-4、互联网和其他资源来获得结果

代理之间相互通信。所以当执行代理完成所有任务，结果不理想时，它可以与任务创建代理通信，创建新的任务列表。三个代理之间的迭代循环，直到完成所有用户定义的目标

AI 代理的行为也显示在用户界面上，将它们分为四组：思想、推理、计划、评判

- 思想（THOUGHTS） ：AI 代理分享它对目标的想法
- 推理（REASONING） ：AI 代理推理如何开展并实现它的想法
- 计划（PLAN） ：AI 代理通过分析，列举了所要完成任务的计划
- 评判（CRITICISM） ：AI 进行自我评判，纠正错误并克服任何限制问题
- 通过共享此计算流程，AutoGPT 可以进行反复尝试论证，并进行针对性的优化处理，可以在没有任何用户干预的情况下克服所遇到的所有问题

## 如何安装 AutoGPT

第一步：下载必备软件
首先你需要有一个 Git 账号，同时需要安装 Python3.1.0 或者更高版本，此外你必须还能熟练使用常用的 shell 命令或者有 Docker 容器进行项目启动和配置

第二步：设置你的 OpenAI API 密钥
打开 OpenAI 帐户后，打开_USER - API keys_转到 API 密钥选项卡。你将看到一个用于创建密钥的选项。单击它，然后复制密钥

第三步：克隆最新版本的 AutoGPT

（1）clone 项目
打开命令行工具通过命令 `git clone https://github.com/Torantulino/Auto-GPT.git` 将项目 clone 到本地

（2）执行安装
通过命令 cd Auto-GPT && ls -al 进入目录后，可以看到有很多的文件，其中一个文件是 requirements.txt。在此文件中，你将看到运行 AutoGPT 所需的模块
要安装这些模块，可以使用命令 pip install -r requirements.txt 进行下载安装

（3）修改配置
通过命令 vim .env.template  进行 open-api-key 的配置 (修改并替换 your-openai-api-key)，配置完成后执行 mv .env.template .env 使配置生效

其他相关的配置可以参考表格按需进行

|配置|说明|
|:---:|:---:|
|LLM PROVIDER | 可以配置 OPENAI_API_KEY，是否使用 AZURE |
|LLM MODEL SETTINGS | 可以配置 openAI 提供的 token 限制，避免过度调用成本浪费 ，默认 4000-8000 |
|LLM MODELS LLM | 底层语言模型，默认可以选择 GPT-4 或者 gpt-3.5-turbo |
|MEMORY | 内存管理，可以配置 local，redis，PINECONE，MILVUS 等 |
|IMAGE GENERATION PROVIDER | 图像生成，可以配置图像大小和图像生成引擎：dalle，HUGGINGFACE，STABLE DIFFUSION WEBUI |
|AUDIO TO TEXT PROVIDER | 语音转文字，可以配置 HUGGINGFACE |
|GIT Provider for repository actions | github 配置，通过配置 github api key 用于访问和管理 github |
|WEB BROWSING | 搜索引擎管理，可以配置不同的浏览器：firefox，chrome，safari，搜索引擎：google 等授权 open api 用于访问互联网获取信息和管理访问深度 |
|TTS PROVIDER | 文本转语音，可以配置 MAC OS，STREAMELEMENTS，ELEVENLABS 来进行文本转语音 |
|TWITTER API | twitter 账号管理，管理配置你的 twitter 账号，配置 token 用于访问对应的 api |
|AUTO-GPT - GENERAL SETTINGS | AutoGPT 的一些默认配置，例如存放目录，开关，user Agent ，AI settings 等 |

（4）开始使用
在完成以上配置以后，就已经完成了 AutoGPT 的基本配置，这时候就可以通过命令 python -m autogpt 开启你的 AutoGPT 之旅 ！

## Docker 使用

当然，你也可以使用 docker 运行 ：

```shell
// 最简单的方式就是通过docker-compose
docker-compose build auto-gpt
docker-compose run --rm auto-gpt

// 使用docker命令构建
docker build -t auto-gpt .
docker run -it --env-file=.env -v $PWD:/app auto-gpt

你可以传递额外的参数，例如，运行方式 --gpt3only 和 --continuous 模式：

// docker-compose
docker-compose run --rm auto-gpt --gpt3only --continuous

// docker 
docker run -it --env-file=.env -v $PWD:/app --rm auto-gpt --gpt3only --continuous
```
