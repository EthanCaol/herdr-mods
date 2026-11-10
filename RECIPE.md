# tab-middle-close

在 Herdr 自带的标签栏上增加两个操作: 鼠标中键关闭标签页, 标签栏末尾的 `+` 直接新建 Claude Code 会话。其余行为与官方 `tabs` 模组一致: 左键切换、左键双击重命名、右键菜单、左键点击 × 关闭。

## 看到的内容

窗口顶部与原版标签栏相同:

- 左侧为标签页, 每个标签显示图标、名称、运行中的转圈标记或等待标记
- 活动标签右侧有 × 按钮
- 右侧为 Files、Changes 面板按钮, Windows 上还有最小化、最大化、关闭三个窗口按钮
- 标签栏末尾(最后一个标签页之后)有一个 `+`
- 底部状态栏不变

## 行为

- 左键按下并松开: 切换标签页, 拖动到另一个标签上可调整顺序
- 左键双击: 重命名标签页
- 右键: 打开标签页菜单
- 左键点击 ×: 关闭该标签页
- **中键点击标签页: 关闭该标签页**
- **点击标签栏末尾的 `+`: 新建一个运行 Claude Code 的标签页**。原来的 `+` 在右侧, 打开程序菜单; 现在改为直接新建会话, 程序菜单不再从标签栏进入
- 关闭最后一个标签页时, Herdr 会弹出确认框, 因为这会关闭整个 space
- 滚轮在标签栏上滚动: 切换上一个或下一个标签页

## 构建方式

- 由官方 `tabs` 模组复制而来(`%USERPROFILE%\.config\herdr-app\mods\tabs`), 增加两处:

```js
// 标签页上中键关闭
.on_mouse_down("middle", (_e, cx) => { cx.stop_propagation(); run("tab.close", { id: c.id }); })

// 标签栏末尾的 +, 直接新建 Claude Code 会话
const newTab = div().id("tab-new").size(24).flex_none().flex().items_center().justify_center().rounded(6).text_color(t.dim)
  .hover(s => s.bg(t.hover).text_color(t.foreground))
  .on_mouse_down("left", stop)
  .on_click((_e, cx) => { cx.stop_propagation(); run("tab.new", { argv: ["claude"] }); })
  .child("+");
```

`newTab` 放到标签栏容器的子元素列表末尾, 跟随标签页一起横向滚动; 原来位于右侧、打开 `new-menu` 的 `+` 已删除。

- 本机布局直接改 `%USERPROFILE%\.config\herdr-app\layouts\main.json`, 把标签栏块的 `content.mod` 从 `tabs` 改为 `tab-middle-close`, 不另建布局
- 窗口按钮图标使用本目录下的 `win-*.svg`, 其余图标引用 Herdr 自带的 `mods/pane`、`mods/files`、`mods/changes`、`mods/workspace-chrome`

## 注意

- 官方 `tabs` 模组每次启动会被 Herdr 覆盖, 所以这里用副本而不是直接改原文件
- Herdr 升级后, 官方标签栏若有新功能, 本副本不会自动获得, 需要重新克隆并合入
- 依赖 Herdr 0.1.14 的 `tabs` 实现

## 完成标准

- `herdr-app check %USERPROFILE%\.config\herdr-app\mods\tab-middle-close` 通过
- 改完布局保存后标签栏正常显示, 标签可切换
- 中键点击标签页后该标签关闭
- 点击标签栏末尾的 `+` 后新标签页打开并运行 Claude Code
