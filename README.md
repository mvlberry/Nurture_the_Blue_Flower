# Nurture the Blue Flower

> To love someone is to nurture a flower.

一个不依赖框架的像素养花小游戏，可直接部署到 GitHub Pages。

播种后会持续出现蓝色和红色流星：点击蓝色流星增加巧克力充能，误点红色流星会扣除充能。充满 100 点后才能使用巧克力，使用后需要重新积攒。页面同时适配桌面和 iPhone 竖屏。

## 本地预览

直接打开 `index.html`，或在项目目录运行：

```powershell
python -m http.server 8000
```

然后访问 `http://localhost:8000`。

## 操作

- 点击“播种”开始。
- 咖啡可直接使用。
- 蓝色流星：充能 `+20`。
- 红色流星：充能 `-20`。
- 巧克力：充能达到 `100` 后解锁，使用后充能归零。
