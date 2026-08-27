# Nurture the Blue Flower

> To love someone is to nurture a flower.

一个不依赖框架的像素告白小游戏。故事依次经过播种、茶餐厅初见、一起玩 Switch、流星夜、蓝花盛开和最终告白，可直接部署到 GitHub Pages。

## 本地预览

直接打开 `index.html`，或在项目目录运行：

```powershell
python -m http.server 8000
```

然后访问 `http://localhost:8000`。

## 修改最终告白

打开 `index.html`，搜索 `FINAL_CONFESSION`，替换该常量中的文字即可。剧情进度保存在浏览器的 `localStorage` 中，右上角“从头再来”可以清除进度。
