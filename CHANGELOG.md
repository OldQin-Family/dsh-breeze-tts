# Changelog · dsh-breeze-tts

> 逐版字节与 SHA-256 见 [FINGERPRINTS.md](FINGERPRINTS.md)。
> 每版详细验收记录见工程内各版工作台的「更新说明」；本表只记版本链与用户可见变化。

## [1.3.0] · 2026-10-30 · 全修复版（含 1.2.0 与 1.1.1 全部内容）

**这一版没有新增功能（除一个 UI 开关），全是修问题**：首轮 13 条（A 串）＋外部回访补充 8 条（B 串）＝ 21 条。

### Changed（安全 / 数据）
- 自动更新附件名不再硬编码旧包名（原整条检查更新链 100% 失效）；`LOCAL_PLUGIN_REPO` 仍为空——面板不显示「检查更新」按钮，更新走插件市场，属**故意未开**。
- `/pair` 加「无局即拒」；配置读损坏一律拒，绝不把读盘失败当成放行。
- `rvc-next` / `rvc-compact-index` / `rvc-packs` 升 write 级；`fetchManifest` 加 1 MB 响应上限（SSRF 收口）；`out_dir` 加 realpath + 相对路径前缀校验，越界拒绝。
- 兑换 `/pair` 前重读磁盘，以盘上为准；工坊预览 blob 全部进回收台账；合成中间 mp3 用完即删 + 启动清扫。
- `GET /config` 改为纯读（损坏改名挪到写路径）；改名失败设 `configCorrupt` 黄条；顶层 `null` = 删键，非法值 400；`dispose?.()` 补 `await`。

### Added
- **唯一功能新增**：`accessMode`（`direct`/`proxy`）两态 UI 开关；`refreshAccessMode()` 从 1.2.0 的死代码接到 5 个入口。
- 跨机配对改用页面内联输入框（原来依赖浏览器原生 `window.prompt()`，部分宿主禁用会直接死）。
- `DEVELOPMENT.md` 文件数 / 行数改为实测值。

### Fixed（外部回访补充 8 条）
- Web Audio 分块循环补三条件 `break`（原缓冲满且无在途时会 200ms 空转死循环，界面卡在「正在朗读」）。
- 工坊 fetch 拆 `workshopFetch`：只对同源 DSH_API 带 token，外部 Breeze 地址用裸 fetch（原 direct 模式会把管理 token 发给外部地址）。
- 工坊三处 blob 补销账（卸载时 / `play()` 抛错时）；`activeChunkQueue` 正常播完也在 `finally` 释放。
- `openai-speech` 路由改走 `speechRoute()`，消除 endpoint 带 `/v1` 时的 `/v1/v1/` 重复拼接。
- `files` 白名单删除已不存在的 `AI_SETUP.md`。
- 共存检测名单分组：上游现名 / 上游旧名（同一项目改名）/ 自家前身私有包，收敛到两个判定函数；实测 7 例全对。

### Notes
- 静态判据 040 为 120/0；043 冒烟 25/0；真机装机重启后零激活错误，`/health` `/config` `/voices` 均 200。

### Known issues（如实带走，非本版引入）
- 重启 DSH 后若浏览器页面未刷新，自动朗读会静默不工作（前端 `configured` 指纹未重连）；手动点朗读正常。临时解法：刷新页面（`Ctrl+Shift+R`）。1.1.1 / 1.2.0 均有，本版未修。
- 工坊面板约 79 处中文字串未接 i18n；约 16 处状态文字切换语言不跟随。
- 音色名不支持中文（Breeze 服务侧硬限制，返回 400）；音色下拉显示 id 而非中文名（接口不返回 `name`）。
- 真机 blob 内存数字、`window.__ModuleLoader__` 里 `options.name` 真机形态未测（代码侧已核）。

## [1.2.0] · 2026-10-30 · 全量审查修复版（含 1.1.1）

上一版 1.1.1 做完第三方全量审查出 40 条发现，本版修完其中「会让用户以为插件坏了」的 21 条：A 类（功能整链失效）7 条、B 类（数据/安全）8 条、C 类其余 6 条。
最主要修复：**音色工坊整条链复活**（1.1.1 里 `breezeApiFetch` 在 `apply` 内定义却在外层调用，工坊打开"连不上"且无报错）。
**1.1.1 从未单独发布**——升到 1.2.0 拿到的是 `1.0.0 + 1.1.1 的 9 条 + 本版 21 条` 合集。

## [1.1.1] · 2026-10-30 · 启动崩溃修复（内测，未单独发布）

- 修 **1.0.0 启动崩溃**：`client.js` 里 `coerceVisibleEngine` 是 `const` 却在定义前被调用（JS 暂时性死区 TDZ），`apply()` 一开头就抛 `ReferenceError`，整个插件加载失败、页面挂。
- 另含 8 条修复；包 25 件。验收 040 115/0、043 27/0 等；真机（酒馆 0.2.0-rc.2 / 19 bundle）三件全过。

## [1.0.0] · 2026-10-29 · 首版

- localtts 与 dsh-plugin-tts 合并 + 新增 AI 可设置通道的首版。
- **已知缺陷**：启动崩溃（TDZ，见 1.1.1），务必升级。
