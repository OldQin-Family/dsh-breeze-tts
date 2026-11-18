# 参考与致谢

> **声明**：本插件的第三方代码来源与许可**逐项列在 [NOTICE.md](NOTICE.md)**（含 MIT 强制要求的逐层版权声明），此处不重复。
> 本文只说明"合并来源"与"未采用代码"的边界，避免两份文书互相矛盾。

## 一、已包含其代码的项目（合并来源，详见 NOTICE）

本插件由以下两个既有插件合并而来，**确实包含了它们的代码**，已按各自许可逐条署名、保留原版权行：

| 项目 | 关系 | 许可 | 声明位置 |
|---|---|---|---|
| [abbccdd/dsh-localtts](https://github.com/abbccdd/dsh-localtts) | 合并主体 | MIT | NOTICE 第一块① |
| [1624318455/dsh-plugin-tts](https://github.com/1624318455/dsh-plugin-tts) | localtts 的上游，MIT 要求逐层声明 | MIT | NOTICE 第一块② |

## 二、只调用服务，未采用代码

| 项目 | 关系 | 许可 |
|---|---|---|
| [breezeblue-ai/breeze-tts](https://github.com/breezeblue-ai/breeze-tts) / 模型权重 `BreezeBlue/breeze-tts-2` | 官方模型与权重；本插件**不含权重**，仅作客户端 | 代码 Apache-2.0；**权重非商业许可** |
| [HoppouAI/Breeze-TTS-2.cpp](https://github.com/HoppouAI/Breeze-TTS-2.cpp) | 实际连接的 C++ 运行时服务；仅通过 HTTP API 调用 | Apache-2.0；MP3 编码器 LGPL-2.0；权重非商业 |

## 三、说明

- 除上述合并来源与运行时服务外，**没有其他需要声明的参考项目**；本插件为这两个插件合并 + 新增 AI 可设置通道而成，未复制其他项目的代码。
- 完整来源、版本、commit 与许可条款见 [NOTICE.md](NOTICE.md) / [NOTICE.en.md](NOTICE.en.md)；逐件字节与哈希见 [FINGERPRINTS.md](FINGERPRINTS.md)。
