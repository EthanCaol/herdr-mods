# herdr-mods

Herdr 桌面应用的模组合集。模组是 Herdr 界面的组成部分, 用 JavaScript 和 gpui-kit 描述原生界面, 保存后热重载。

## 安装

把模组文件夹复制到 Herdr 的模组目录:

```
%USERPROFILE%\.config\herdr-app\mods\<name>\
```

然后在 Herdr 里打开:

```
herdr-app do mod.open --name <name>
```

或者用带参数的模组面板: `pane.split` 时传 `mod` 与 `props`。

## 模组列表

| 模组 | 说明 | 安装 |
| --- | --- | --- |
| `tab-middle-close` | 标签栏增加鼠标中键关闭标签页 | 复制 `mods/tab-middle-close` 与 `layouts/main-middle-close.json`, 然后 `herdr-app do layout.switch --name main-middle-close` |

## 目录

```
mods/<name>/
  main.js       模组本体(必需)
  mod.json      首次出现的位置: {"place": "right" | "left" | "top" | "bottom" | "none", "size": 320}
  RECIPE.md     说明文件, 供他人重写或参考
  preview.png   截图
```

## 说明

- Herdr 自带的模组是只读的, 启动时会被覆盖。要修改, 先用 `herdr-app do mod.clone --name <name> --as <new-name>` 复制一份
- 接口文档在 `%USERPROFILE%\.config\herdr-app\AGENTS.md`, 类型定义在同目录的 `gpui-kit.d.ts` 与 `herdr.d.ts`
- 模组是受信任的代码, 可以访问网络、执行命令、读写文件

## 许可

各模组如无单独说明, 按 MIT 许可使用。
