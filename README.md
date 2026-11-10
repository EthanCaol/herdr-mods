# herdr-mods

个人使用的 Herdr 模组, 目前只有一个: 标签栏支持鼠标中键关闭。

模组是 Herdr 界面的组成部分, 用 JavaScript 和 gpui-kit 描述原生界面, 保存后热重载。

## 安装

把本目录复制成 Herdr 模组目录下名为 `tab-middle-close` 的文件夹:

```
git clone https://github.com/EthanCaol/herdr-mods.git tab-middle-close
move tab-middle-close %USERPROFILE%\.config\herdr-app\mods\
```

再复制一份官方布局并启用:

```
herdr-app do layout.clone --name main --as main-middle-close
herdr-app do layout.switch --name main-middle-close
```

打开 `layouts/main-middle-close.json`, 把标签栏块的 `content.mod` 从 `tabs` 改为 `tab-middle-close`。改动保存后热重载生效。

## 文件

| 文件 | 作用 |
| --- | --- |
| `main.js` | 模组本体, 由官方 `tabs` 模组复制后增加中键处理 |
| `mod.json` | 模组属性: 放置位置 `none`, 标题 `Tabs` |
| `win-*.svg` | Windows 上的最小化、最大化、还原、关闭按钮图标 |
| `RECIPE.md` | 改动的说明, 以及 Herdr 升级后重新合入的步骤 |

## 说明

- Herdr 自带的模组是只读的, 启动时会被覆盖。要修改, 先用 `herdr-app do mod.clone --name <name> --as <new-name>` 复制一份
- 接口文档在 `%USERPROFILE%\.config\herdr-app\AGENTS.md`, 类型定义在同目录的 `gpui-kit.d.ts` 与 `herdr.d.ts`
- 模组是受信任的代码, 可以访问网络、执行命令、读写文件

## 许可

MIT
