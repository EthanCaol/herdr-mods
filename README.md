# herdr-mods

个人使用的 Herdr 模组, 目前只有一个: 标签栏支持鼠标中键关闭, 末尾的 `+` 直接新建 Claude Code 会话。

模组是 Herdr 界面的组成部分, 用 JavaScript 和 gpui-kit 描述原生界面, 保存后热重载。

## 安装

把本目录复制成 Herdr 模组目录下名为 `ethancao` 的文件夹:

```
git clone https://github.com/EthanCaol/herdr-mods.git ethancao
move ethancao %USERPROFILE%\.config\herdr-app\mods\
```

再复制一份自带布局并改内容:

```
herdr-app do layout.clone --name main --as custom
```

打开 `layouts/custom.json`, 把标签栏块的 `content.mod` 从 `tabs` 改为 `ethancao`, 然后 `herdr-app do layout.switch --name custom`。自带布局 `main` 每次启动会被 Herdr 重写, 所以必须用副本。

## 配色

`themes/one-half-dark.json` 是 Windows Terminal 的 One Half Dark 配色, 复制到 `%USERPROFILE%\.config\herdr-app\themes\` 后, 在 `layouts/custom.json` 根节点写 `"theme": "one-half-dark"`, 或执行 `herdr-app do app.theme --name one-half-dark`。

## 文件

| 文件 | 作用 |
| --- | --- |
| `main.js` | 模组本体, 由官方 `tabs` 模组复制后增加中键关闭与末尾 `+` 新建会话 |
| `mod.json` | 模组属性: 放置位置 `none`, 标题 `Tabs` |
| `win-*.svg` | Windows 上的最小化、最大化、还原、关闭按钮图标 |
| `plus.svg` | 标签栏末尾的加号图标 |
| `themes/one-half-dark.json` | One Half Dark 配色, 背景 `#282c34`, 前景 `#dcdfe4` |
| `RECIPE.md` | 改动的说明, 以及 Herdr 升级后重新合入的步骤 |

## 说明

- Herdr 自带的模组是只读的, 启动时会被覆盖。要修改, 先用 `herdr-app do mod.clone --name <name> --as <new-name>` 复制一份
- 接口文档在 `%USERPROFILE%\.config\herdr-app\AGENTS.md`, 类型定义在同目录的 `gpui-kit.d.ts` 与 `herdr.d.ts`
- 模组是受信任的代码, 可以访问网络、执行命令、读写文件

## 许可

MIT
