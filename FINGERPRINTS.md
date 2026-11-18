# 发布件逐件校验清单（dsh-breeze-tts v1.3.0 · GitHub 整理版）

本表列出本发布目录 **58 件**的字节数与 SHA-256，供逐件独立复算；件数与内容以本目录为准。

> 本文件（FINGERPRINTS.md）与发布压缩包（zip）自身**不计入**本表，避免自指。

复算方式（任选其一）：
1. 本地现算：`sha256sum <文件>`（Windows：`Get-FileHash -Algorithm SHA256`）。
2. 走 API（仓库公开后）：`GET https://api.github.com/repos/OldQin-Aurora/dsh-breeze-tts/contents/{path}` → `.content`（base64）解码现算；`.sha` 是 Git blob 号，**不是**本表的 SHA-256，两者不可混用。

| # | 路径 | 字节 | SHA-256 |
|---:|---|---:|---|
| 1 | `.gitattributes` | 372 | `c77eaa63a1d6b0f216082f579c30d9f8b40910397a3588b60ee983036bd81cfa` |
| 2 | `.gitignore` | 6 | `15093ccf76e1aa623e0fe9d23172fa6cdf29131a772d2eb49bae10708e1e6434` |
| 3 | `ACKNOWLEDGEMENTS.md` | 1732 | `c02bb7b316396f2013e732480461b342b53c6d73d4cdd07155f2ad10647646eb` |
| 4 | `CHANGELOG.md` | 4408 | `baa1f180dbdb6733eba80b61b14130e5d502a47c2d27a5d8ce4a3523e968c9b3` |
| 5 | `DEVELOPMENT.md` | 23688 | `f43e1be4b14cba786a0db453d9f3a0fafd011eab7a4debc37ca8bd3dab74456e` |
| 6 | `HARDWARE.md` | 14016 | `74bf5dd64996431a8ead292b98c94b4b16c095c5ee73f364d136fa6e66b9e111` |
| 7 | `LICENSE` | 3591 | `decc69ad863d130a8103a2489af58d89e6a83fc6c3fe15cc4ba87a3af99a6cf2` |
| 8 | `NOTICE.en.md` | 5087 | `a9b7675fa4da0ef2f67a37688112beb2c18adf4b8c128b9e307013788e464661` |
| 9 | `NOTICE.md` | 4788 | `d76131b2b2a30d723d6c1d0e62777c89716c5171041129e624b2c2340b10eeed` |
| 10 | `README-AI.md` | 34883 | `148c85e6dec9024845e99cbf6c6560a070d99f592a5ad23130e3c6c250ab8eeb` |
| 11 | `README.en.md` | 15927 | `c4d243e9128288d1bf321a3c1825853e9d7014a2a5293910d91009cf3305d2d9` |
| 12 | `README.md` | 22620 | `e51d80b3d3bebca9bf475aa553505cf9e220c261e201244fe3e4f3342ff1f2ba` |
| 13 | `SKILL.md` | 8749 | `549783b0ce8f5d2113cda38a7119916601e4b232dc9c54593718c46982c9fedb` |
| 14 | `assets/brand/icon-breeze-512.png` | 7728 | `fe11cc7184ac5ee0f82b03c6188458e36a56d37b084eda66ca7b9b983cbdf5a9` |
| 15 | `assets/brand/icon-breeze.svg` | 1044 | `b3628449a9dff851f4bfee61fd8508943ff9bfdbc0d5ff976c6340b80db27490` |
| 16 | `assets/team/avatar-ashu.png` | 404750 | `6991e2730d8a5f7d2a95ab5d0eaab647620cd1a6ca4e6cd3bca4cd3e9a296224` |
| 17 | `assets/team/avatar-azi.png` | 450855 | `09e4c85fb34af76d8ad26b245fa2f2cb305689ac36bc6503edf42f25a3b6c57a` |
| 18 | `assets/team/avatar-daa.png` | 480997 | `42ce7798acac3ea4162457b37221da0397ce773ce0f0161ca6cd162a1bb6b689` |
| 19 | `assets/team/avatar-daniu.png` | 424143 | `accbf839ffd63c20b3de2fe469b26243870ba057857c4592da2b4cdf5386f7a8` |
| 20 | `assets/team/avatar-laodou.png` | 440813 | `8da0fac1dc6d51d20e7f4a08f40cc5f4a05850c8774590911e32780b34422250` |
| 21 | `assets/team/avatar-laohuojie.png` | 15237 | `cf9d0922955533f33cd1525204510a27f45955a5892335c2ebf5db723a4a4c3f` |
| 22 | `assets/team/avatar-laoqin.png` | 413944 | `9486a71acc0e5b3edd966422a04aab69a0ca0a674c1e6d552ee0318ea3bdab13` |
| 23 | `assets/team/avatar-neko.png` | 598216 | `ffdc7c219f856d87e34a1185506a5a60018c5a366f25e0768fe9cd8e3aa755ef` |
| 24 | `assets/team/avatar-pro.png` | 476518 | `7c30cafd71353af9905935cbef45ec65e01ae4e2662000e5f97457a8fdb4dbf1` |
| 25 | `assets/team/avatar-turbo.png` | 417620 | `030a4d2034a3c1ced6c32ffdfb58dde66b3fd49bdd427b682670405f66993efd` |
| 26 | `assets/team/avatar-xiaoa.png` | 384312 | `b32eea394a523019dca435710cfa30161ab3a65ef485388389eb5253642bfaa1` |
| 27 | `assets/team/avatar-xiaoniu.png` | 492048 | `c6a8df9a02e908793c76d5395ff617abf3f28c3a82c0ee4749b9f7220c971b97` |
| 28 | `assets/team/avatar-xiaoshen.png` | 411902 | `65a3ff74c5207d06c724ed5b0ba2aca9ead39836e93917f6b1b76b4073cbfa6b` |
| 29 | `assets/team/avatar-xiaoshu.png` | 14594 | `c786ffc299f59d886b0e6f8d700aa96ebe16c97726a2d09348632cb7f8ebba2c` |
| 30 | `assets/team/avatar-zhuazong.png` | 15701 | `742c9dd5482a190ab8ab42c05dd6dc68f869fcaf813239179a4388fe92c16e59` |
| 31 | `assets/截图/README.md` | 726 | `a77e541001cf5881a555a6cf403379ef78b0735f234923ba8814359a855050a2` |
| 32 | `assets/截图/settings.png` | 141730 | `3b830821bb20a76c78baafc912bd13c31715a2570060eb7725949d40267af5da` |
| 33 | `assets/截图/workshop-clone.png` | 60641 | `430150caee974c8b9f40cd092ecbb660362ce05d8eb75d1015c6d4951656261e` |
| 34 | `assets/截图/workshop-design.png` | 99822 | `89cce862250b9c117c35b10dc1aca166891485d3bf877e754c85360f482081a4` |
| 35 | `assets/流程图/BreezeTTS_workflow-en_v1.3.0.png` | 520037 | `4fa03f5f5e67ea0441295144ba02d2187b921f93fa01a4e2c2d2938eebcbe5c3` |
| 36 | `assets/流程图/BreezeTTS_workflow-en_v1.3.0.svg` | 65045 | `4357beb5c2ff3e3799e5968c2c42584b2a55fbcc3c9fd66c8b598059a6fd4bbc` |
| 37 | `assets/流程图/BreezeTTS_整机流程图_v1.3.0.png` | 574707 | `caaf3ebaee1be8b55027048cc6f9d4daef0d2fe19f9c557c6778ccd762bcd759` |
| 38 | `assets/流程图/BreezeTTS_整机流程图_v1.3.0.svg` | 75586 | `0f9679d0347f3dce247b9b7a4c0e73c3c1a6df0d789edd21c6f95116cfc54dcd` |
| 39 | `cordis.patch.yml` | 123 | `339257c6ad862b5e64c403fc87516606ad8090c50906a81699dda15fa80e7133` |
| 40 | `icon.png` | 3287 | `c6d372feffd2cbf636012cb38984dd9428ccd308311380607f149f5b720cbd87` |
| 41 | `index.html` | 3238 | `7d0d868e84e8186ef580ef1956e67a9a3e5ed61ab555662646f7a5a9a424b0d7` |
| 42 | `lib/client.js` | 350737 | `00e49f20b02a3a47642f9138646c6e14520d5b0576e692dda55e99bf897ef6a5` |
| 43 | `lib/coexistence.mjs` | 2493 | `5c9a48244b668de14665f87062666d63f8725e4af5692fa0eb1db17ef68a6240` |
| 44 | `lib/index.mjs` | 113344 | `5bb0a1c410f7122b2cde14a0095d0028ac975b226af618c994526636060bfb27` |
| 45 | `lib/local-runtime/discovery.mjs` | 10725 | `2041c5e3ff7c88c1830f4f7f1dc74de194368539f7dfa52facb98997151ce4f9` |
| 46 | `lib/local-runtime/errors.mjs` | 111 | `220749bd6f05a79825d2ddcb4c1c51bbc6b68868b4650a082aa7a25f895d5b15` |
| 47 | `lib/local-runtime/http-profile.mjs` | 8047 | `321aab6eee31df1108eb11218f50558df9bed2bf4ec2b4d681284e55064ae357` |
| 48 | `lib/local-runtime/model-discovery.mjs` | 6849 | `387aa405986ec18e18dbb9c395f3223ead4d9e0ea14c3555508d00395a0fb4f7` |
| 49 | `lib/local-runtime/provider.mjs` | 33375 | `3a87ef802edf216c972af5a6d81bfcf9c2b7230697e82bf63a19cae12136f7df` |
| 50 | `lib/local-runtime/runtime-pool.mjs` | 3602 | `8d6668da9501229cc05a5ec98f19778b5cee3ed79c3735c39b07b02126daca43` |
| 51 | `lib/local-runtime/sentence-buffer.mjs` | 2859 | `689dbec3dc69fa22d3803fd91fd399a1acf121eb2264ae17232c1cc3ccb4b9f8` |
| 52 | `lib/local-runtime/service.mjs` | 14796 | `b4f7e9ef10a19338a682ecd156607587dde9212406d80004444797c86de5d44a` |
| 53 | `llms.txt` | 7335 | `4fd31211ca64e4e3b1246444565fbe45294ebe20abb4b753438f9378166354f5` |
| 54 | `package.json` | 1294 | `1bb8bf9a89c4c00644723d08f3afa5137baf2bad7a05775f03fa01b5560b70d1` |
| 55 | `screenshots.json` | 112 | `c624fd9cbc73517ab50dd73e2c80776e22c912367cee4c952f1ec5ba3f8cf5ea` |
| 56 | `site.json` | 7911 | `ad4c4ac5a762b45b2dfa405dc88965b2e394447a623405f38419f2430659e790` |
| 57 | `tools/verify-modes.mjs` | 13816 | `25773473fbf5c29259c06be20ecad81336010719398a806eaba772f7314ac797` |
| 58 | `使用说明.md` | 2096 | `876c871c8c68f91f3caf2f46745edba4adf55c47f16b2632bf109b4940a2b7af` |

**合计**：58 件 / 7714733 字节。

> 本表为补件归位后全量现算：补入 15 张家人墙头像（与标准素材库逐字节一致）、截图归位到 `assets/截图/`、新增 CHANGELOG／NOTICE.en／ACKNOWLEDGEMENTS／使用说明／index.html／.gitattributes；中英 README 加家人墙与目录、全库截图路径与界面入口口径同步。
> 四件流程图为冻结放行件，字节与 sha8 未动：`CAAF3EBA`（中 PNG）／`0F9679D0`（中 SVG）／`4FA03F5F`（英 PNG）／`4357BEB5`（英 SVG）；详见上表对应条目。
> **条件件 N/A 立牌**：`隐私与合规说明.md` — N/A，本插件为 TTS 客户端，不监测、不采集、不上报，不触发隐私/监测类必选条件；`packages/dsh-*` — N/A，本包自身即 DSH 插件（整包即插件），无「本体＋可选插件」两层结构；`启动*.bat` — N/A，本插件是浏览器客户端，非 Windows 直跑程序；`tests/` — 以 `tools/verify-modes.mjs` 自检脚本替代。
> 发布压缩包 ZIP 单独报指纹，不计入本表。
