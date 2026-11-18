---
name: dsh-breeze-tts
version: "1.3.0"
author: OldQin Family
license: MIT
metadata:
  tags: [dsh-plugin, tts, breeze, voice, local-runtime, cross-machine]
description: "Use when 装/配/排障 DSH 的 Breeze 语音插件（dsh-breeze-tts）、判断机器跑不跑得动 Breeze TTS、造/克隆音色、或处理跨机 403/401；or when the user asks about dsh-breeze-tts setup, Breeze TTS endpoint, voice design/clone, or remote access — 先读本 skill 的最短路径与铁律，详细作业再读 README-AI.md。"
---

# dsh-breeze-tts · Breeze 语音使用口径（中文）

> **DSH 语音插件**（本包所在目录：`README.md` / `README-AI.md` / `HARDWARE.md` / `lib/` 都在这里）。
> 完整说明在**本包 `README.md`**；**安装/配置/接口/排错的详细作业在 `README-AI.md`**；本 skill 是"遇到这类任务时的最短正确路径 + 铁律 + 排雷"。
> 维护者：OldQin Family（「老秦 Family」）。语言：简体中文。版本：1.3.0。MIT。

## 何时用本 skill

- 用户要**装**这个插件（刚下载、还没进 DSH）；
- 用户要**配** Breeze 服务地址、设音色、开自动朗读；
- 用户要**造音色 / 克隆音色 / 管理音色**；
- 用户问**这台机器跑不跑得动**、该下哪个量化档；
- 用户遇到 **403 / 401 / 连不上 / 音色下拉空 / 试听没声**；
- 用户要做**跨机调用**、问 remoteAccess / token / 配对码怎么用。

## 铁律（先读这个再动手）

1. **它只是客户端，不自带模型** —— 插件自己不出声，连用户另起的 Breeze 服务才出声。**服务没有≠插件坏了**，先探 `GET <breeze>/health`。
2. **不替用户装 Breeze 服务** —— 那是几 GB 权重＋显卡驱动的活，插件做不了，别许诺。
3. **先判装没装，再决定从哪节开始** —— 查 DSH profile 的 `dependencies` 和 `node_modules/dsh-breeze-tts`，两条都命中＝已装（去配置），都没命中＝没装（去安装）。别上来就改。
4. **配置是 host 侧单一真源** —— `~/.dsh/dsh-breeze-tts/config.json`，界面和 AI 都读写它。改配置**禁止整包覆盖**：只写 `localRuntime` 等子键，否则别的子键（autoRead/voice/rvc/notify）全丢。写完必须 `GET /config` 回读逐字段核对。
5. **默认只本机可用，403 是特性不是故障** —— `remoteAccess=false` 时非本机一律 403。开远程后**写**接口要 Bearer token。
6. **穿透必须开 `requireLocalToken=true`** —— frp/ngrok/cloudflared 这类反代会把来源伪装成 `127.0.0.1`，绕开"本机"判定；VPN 类（Tailscale/ZeroTier）不伪装，不必开。
7. **`trustedLocalCidrs` 不是放行名单，是"视为本机名单"** —— 加 IP＝把对方当本机（免 token 且能拿到 token）。不经用户明确同意，不往里加。
8. **测完远程开关必须复位** —— `remoteAccess` / `requireLocalToken` 用完恢复 `false/false` 并重启，否则留安全口子或把所有人挡在 401 外。
9. **token 只住 `config.json`** —— 不写进任何会被提交/分享的文件。
10. **音色 id 不许凭记忆假设** —— 先 `GET /voices` 列出真实返回，`GET /config` 也不返回 token（防穿透，故意的）。
11. **声音好不好听只能人听** —— 程序只能证明"出了一段合法 wav"，别替用户判断音质。
12. **不改插件源码、不动别的 DSH 实例和别人的配置** —— 要改行为先报维护者；旧插件卸载要有人拍板。

## 最短路径（判断 → 干活 → 自证）

### 第一步：判断走哪条

```
# <DSH_HOME> 是含 profiles/web 的那一级
grep -n "dsh-breeze-tts" "<DSH_HOME>/profiles/web/package.json"
ls -d "<DSH_HOME>/profiles/web/node_modules/dsh-breeze-tts"
```

| 情况 | 去做 |
|---|---|
| 机器能不能跑都不知道 | `HARDWARE.md` §5 五步判定，或 README 的「情况 C」话术 |
| 两条都没命中（没装） | `README-AI.md` §1 安装 → §2 配置 |
| 都命中（装好了） | `README-AI.md` §2 配置（8 条 REST） |

### 第二步：记住两个地址和三个事实

- Breeze 服务默认 `http://127.0.0.1:8080`，健康检查 `GET /health` → `{"status":"ok",...}`；
- 插件接口前缀 `/dsh-breeze-tts-api`，挂在 **DSH 宿主端口**（默认 3104，但每个实例可能不同——先看启动参数或 `netstat -ano` 确认，别想当然）；
- `$API = http://127.0.0.1:<DSH端口>/dsh-breeze-tts-api`。
- 音色数量**以 `/voices` 返回数组长度为准**，不假设任何 id 存在。
- 版本真值两处：`package.json` 的 `version` 与 `lib/client.js` 的 `LOCAL_PLUGIN_VERSION`，都是 `1.3.0`（不一致就是被改坏了）。

### 第三步：常用命令（从 README-AI.md §2 摘最短的）

```bash
# 健康检查（Breeze 通不通）
GET  <breeze>/health

# 读配置 / 写配置（局部 merge，别整包覆盖）
GET  $API/config
PUT  $API/config     -d '{"localRuntime":{"endpoint":"http://127.0.0.1:8080"}}'

# 列音色 / 试听
GET  $API/voices
POST $API/speak-preview -d '{"text":"你好，测试一下","voice":"<真实id>"}'

# 造音色（描述） / 克隆（音频+逐字转录） / 删
POST   $API/voices/design    # 描述造音色，详见 README-AI.md §2 ⑥
POST   $API/voices/clone     # multipart: ref_audio/ref_text/name，详见 §2 ⑦
DELETE $API/voices/<id>      # 删音色，详见 §2 ⑧

# 跨机首次配对：在 DSH 本机生成 6 位一次性码，另一台兑换 token（不挂鉴权，故意的）
POST   $API/pair/new         # 本机生成 code
POST   $API/pair             # 另一台用 code 换 token
```

> Windows 命令行带中文：**PowerShell 用单引号包住**，或**写文件再 `--data-binary`**（PS 5.1 别加 BOM，用 `-Encoding ascii`）。Bash/Git Bash 用反斜杠转义。详见 `README-AI.md` §2 ⑤。

### 第四步：自证（缺一步不算完成）

1. 改配置 → `PUT` 后 `GET` 回读，逐字段核对；
2. 设音色 → 回读 `voice` 字段 **＋** `POST /speak-preview` 真出一段 wav；
3. 造/克隆 → `GET /voices` 出现新 id **＋** 试听可用；
4. 装插件 → 指纹全一致 **＋** 启动日志无报错 **＋** DSH 设置里能看到两个入口：「Breeze 设置」（共存态「本地语音」）与「Breeze 音色工坊」。

**每步把命令与返回原文整理给人，不要只报"配好了"。**

## 常见误判排雷

- **403** ≠ 装坏了：非本机且 `remoteAccess=false`，特性。到本机执行或按 §6 开远程。
- **401** ≠ token 错了就重试：可能是 `requireLocalToken=true`，或写接口没带 Bearer；token 从 `config.json` 读（`GET /config` 不返回，故意的）。
- **音色下拉空** ≠ 插件 bug：官方 PyTorch 版没有 `/v1/voices`，下拉必空；换 C++ 版或手填 id。
- **配置一直不生效**：DSH 进程的 `homedir` 可能不是你以为的那个（SYSTEM 跑时常见）——见 `README-AI.md` §4「配置路径坑」。
- **`GET /config` 看不到 token**：不是丢了，是远程请求或穿透模式下故意不下发；本机直接读文件。
- **409**：Breeze 单并发，上一个没完，等 2 秒重试（UI 侧已自动重试一次）。
- **音色名报 400**：名字带中文或符号；只用 `[A-Za-z0-9_-]`（Breeze 服务侧硬限制，插件改不了）。
- **`[笑]`/`[叹气]` 没触发**：事件标签要 `cfg_scale` 2–3 才真触发，默认 1.0 多半平着念。
- **旧版配置整块被清**：旧包写 `speech` 是整块替换（2026-10-29 已修）；连旧包时传子集会丢别的子键。

## 安全与禁止（转述/执行都守）

- ❌ 不把 Breeze 服务挂公网（官方无鉴权、无限速）；
- ❌ 不用 frp/ngrok 暴露端口还不开 `requireLocalToken`；
- ❌ 不把 token 写进会提交/分享的文件；
- ❌ 不绕过鉴权矩阵（隧道伪装来源）；
- ❌ 不自己决定卸旧插件（有人拍板才行）；
- ❌ 不动别的 DSH 实例、别人家的配置；
- ❌ 不改插件源码（要改行为先报维护者）；
- ❌ 不替人判断"声音好不好听"，也不许诺插件能装 Breeze 服务。

## 口径真源（有出入时以哪个为准）

- **产品行为与功能**：本包 `README.md` + `README-AI.md`；
- **硬件判定**：`HARDWARE.md` §5（官方没给的数字照实说"官方没给"，不编）；
- **配置/接口/鉴权真码**：`lib/index.mjs`（host 侧）与 `lib/client.js`（界面侧），及 `package.json`；
- **机器可读事实**：`site.json` 是索引，不是真源；`llms.txt` 是说明与边界。
- **许可与来源**：`NOTICE.md` / `LICENSE`——运行时依赖的 Breeze 模型权重是**非商业**许可，分发/商用前先读。
