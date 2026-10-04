# BalancePet 形象仓库

[English](README.en.md)

BalancePet 的形象包都在这里发布。形象就是桌宠画出来的那个角色；装上一套之后它会出现在
设置的形象选择器里，可以随时切换、停用和卸载，都不需要动主程序。

## 📦 安装

1. 从 [Releases](../../releases) 下载想要的那套形象的 ZIP。
2. 在 BalancePet 里打开 **设置 → 扩展**。
3. 把 ZIP 拖进本地扩展区。

不需要重启，形象会立刻出现在选择器里。

卸载在同一页做，方式一样。内置占位形象不能卸载：**角色就是窗口本身**，一套都不剩的安装
会显示一个空白窗口，界面上也没有退路。把自己装的形象全卸掉是没问题的 —— 剩下的就是占位
形象，它也是什么都没装时窗口画的东西。

## 🎭 形象列表

| 包 | 形象 | 美术名 |
| --- | --- | --- |
| `pet.deepseek` | DeepSeek 小鲸鱼「澜汐」 | DeepSeek Whale "Lanxi" |
| `pet.chatgpt` | ChatGPT 小白龙「霁珑」 | ChatGPT White Dragon "Jilong" |
| `pet.minimax` | MiniMax 小海螺「绯音」 | MiniMax Shell "Feiyin" |
| `pet.gemini` | Gemini 小星猫「星璃」 | Gemini Star Cat "Xingli" |
| `pet.grok` | Grok 小恶魔「烬斧」 | Grok Little Demon "Jinfu" |
| `pet.claude` | Claude 小书灵「丹笺」 | Claude Little Book Spirit "Danqian" |
| `pet.kimi` | Kimi 小棱镜「虹谱」 | Kimi Little Prism "Hongpu" |
| `pet.qwen` | Qwen 小折扇「绀华」 | Qwen Folding Fan "Ganhua" |
| `pet.ernie` | Ernie 小病书灵「青绡」 | Ernie Little Book Spirit "Qingxiao" |
| `pet.glm` | GLM 小方灵「青棱」 | GLM Little Square Spirit "Qingleng" |
| `pet.gpt-image2` | GPT Image 2 小墨龙「玄珏」 | GPT Image 2 Ink Dragon "Xuanjue" |
| `pet.llama` | Llama 小羊驼「绒眠」 | Llama Alpaca "Rongmian" |
| `pet.mimo` | MiMo 小兔码师「橙析」 | MiMo Bunny Coder "Chengxi" |
| `pet.mistral` | Mistral 小猫骑士「麦霜」 | Mistral Cat Knight "Maishuang" |
| `pet.opencode` | OpenCode 小码灵「墨枢」 | OpenCode Code Sprite "Moshu" |
| `pet.perplexity` | Perplexity 小探灯「青鉴」 | Perplexity Little Lantern "Qingjian" |
| `pet.rwkv` | RWKV 小夜鸦「夜翎」 | RWKV Little Raven "Yeling" |
| `pet.seedance` | Seedance 小星晶「澄芽」 | Seedance Little Star Crystal "Chengya" |

BalancePet 画的每一套形象都在这里发布，包括 v1.4.3 之前随安装包分发的 DeepSeek 小鲸鱼
「澜汐」和 ChatGPT 小白龙「霁珑」。唯一不发布的是内置占位形象：它是什么都没装时窗口画的
形状，所以它必须是永远不会缺的那一套。

主程序曾经自带的形象按原样发布，这样升级上来的安装能保住正在用的角色：包里 `style` 的值
与主程序一直保存的标识符相同，设置才能继续解析。

## 💬 台词

每个包都带着角色的台词，所以它不联网也会说话。同一份台词还会汇总到本仓库的
[`lines.json`](lines.json)，主程序能联网时优先用它 —— 一个包几乎全是美术，为了改一句话
重发一次，等于让每个安装都为几百字节下载几兆。

每套形象还有一句介绍，随目录条目一起发布，在商店里显示在名字下方。那些介绍写主程序的
[`appearance-copy.json`](appearance-copy.json)，因为一句关于角色的话不该住在十二兆美术里。

## 🖼️ 商店里显示的图

在线列表里会有本机还没装的形象，所以它没有美术可画。每个条目因此指向 [`previews/`](previews)
里的一张方形头像：**手绘的大头图**，圆角方底，取自角色自己的配色 —— 而不是从立绘里裁出来的，
立绘缩到 32 px 的一行里，脸只剩七分之一格。

已经装上的形象也用同一张图，两边长得一样。这套头像同时用于在线列表和已安装列表，所以商店里
看到的和桌面上跑的是同一个形象。主程序把下载过的图标缓存在本机（按条目与版本为键），在
**设置 → 高级与迁移** 里可以看到占用并清除。

## 📁 包格式

格式由[资源扩展规范 v1](https://github.com/GoldenMoon-cell/BalancePet/blob/main/docs/extension-spec/v1/README.md)
定义。简单说，一个包就是包含这些文件的 ZIP：

```text
manifest.json
assets/pets/<style>/idle.png
assets/pets/<style>/loading.png
assets/pets/<style>/success.png
assets/pets/<style>/low.png
assets/pets/<style>/error.png
assets/pets/<style>/clicked.png
assets/pets/<style>/codex-working.png
assets/pets/<style>/codex-done.png
assets/pets/<style>/inactive.png
```

九张状态图全部必需。它们必须是共享同一画布的透明 RGBA PNG；内置形象用的是 238 × 238。

资源包永远不会被执行。主程序只读 PNG 和清单，别的什么都不读，所以包里不可能有代码；也不
限定画风、配色或角色方向 —— 只要求上面这份文件契约。

## 🔨 打包

打包脚本在主程序仓库：

```powershell
.\tools\package-pet-extension.ps1 -SourceDirectory .\pet.example -OutputPath .\dist\pet.example-1.0.0.zip
```

## 🤝 贡献形象

投九张状态图之前，先开个 issue 附一张预览。九种状态不是可以互相顶替的：`low` 和 `error`
是一眼扫过的，不读气泡也要能分辨；`inactive` 是压暗画的，所以还得看出是同一个角色。

不要提交版权或许可不允许再分发的美术。BalancePet 自己的角色参考在它的
`THIRD_PARTY_NOTICES.md` 里署名；在这里贡献的形象必须是你有权授权的，或者带着允许的许可。