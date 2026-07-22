# Mineradio 飘雪预设补丁

给 Mineradio (XxHuberrr/Mineradio) 添加一个"飘雪"视觉预设（preset 7）。

## 用法

1. 安装 Mineradio 桌面版（v1.1.1）
2. 备份 `resources/app/public/index.html`
3. 把原始 `index.html` 替换为 `mineradio-snow-preset.patch` 打补丁后的版本，或者直接用本仓提供的 `index.html.patched`
4. 重新启动 Mineradio
5. 打开视觉控制台 → 预设 → 选"飘雪"

## 补丁内容

`mineradio-snow-preset.patch` 是针对原版 `index.html` 的 unified diff，包含：

- `presetMeta` 数组增加 `{ name: '飘雪', desc: '雪花 · 静谧飘落' }`
- `presetIcons` 增加雪花图标
- `presetDisplayOrder` 增加 7
- 顶点着色器 if/else 链增加 snow 分支（else if < 6.5 → else）
- snow 分支：粒子从 y=7 飘到 y=-7，横向 wobble + drift，bass 加速
- 片元着色器：snow 跳过 readableRim 黑边逻辑（避免雪看起来脏）
- vBright guard：snow 保持 ≥0.90 亮度
- size 公式：snow 用 `depthSize * sizeVar * 0.55`
- 28% 粒子显示为雪（`aRand > 0.28` 的隐藏），其余隐藏

## 相关修改

- `coverResolution` 建议从 1.55 降到 1.0（粒子 33k→14k），启动 splash 明显更流畅
- `index.html.patched` 是已经打好补丁的完整文件（26k+ 行）

## 原始项目

- GitHub: https://github.com/XxHuberrr/Mineradio
- 官网: https://mineradio.cn/
- 在线版: https://mineradio.art/

## 许可证

补丁基于原项目，遵循原项目许可证。
