# 棋牌 PWA（象棋 + 麻将何切）

两个单文件游戏打包成一个可安装的 PWA：装到桌面/主屏幕后全屏运行，首次打开后离线可用。

## 目录

```
qipai/
├── index.html          入口页（象棋 / 麻将两个入口）
├── xiangqi.html        中国象棋（源：中国象棋/xiangqi.html）
├── heqie.html          麻将何切（源：麻将/heqie.html）
├── manifest.json       PWA 清单
├── sw.js               Service Worker（缓存）
└── icons/              192 / 512 / apple-touch-icon
```

## 本地预览

必须用 http 打开（`file://` 下 Service Worker 不工作）：

```bat
python -m http.server 8002 --directory qipai
```

然后访问 http://127.0.0.1:8002/

## 部署到 Gitee Pages

1. Gitee 新建一个**公开**仓库（例如 `qipai`），完成实名认证（Pages 要求）；
2. 把 `qipai/` 里的**全部文件**上传到仓库**根目录**（index.html、xiangqi.html、heqie.html、manifest.json、sw.js、icons/）；
3. 仓库页 → 服务 → Gitee Pages → 部署分支选 `main`、部署目录选 `/` → 启动；
4. 等构建完成，访问 `https://<你的用户名>.gitee.io/qipai/`；
5. 以后每次改了游戏文件，都要回 Gitee Pages 页面点一次「**更新**」，否则线上还是旧版。

## 安装

- 安卓 Chrome / Windows Chrome、Edge：地址栏或菜单里选「安装应用 / 添加到主屏幕」；
- iOS Safari：分享 → 添加到主屏幕。

## 注意

- Service Worker 必须跑在 https 或 localhost；Gitee Pages 是 https，满足条件。
- 微信内置浏览器不显示安装入口，让对方「右上角 → 在浏览器打开」。
- 改了前端文件后，建议把 `sw.js` 里的 `CACHE = "qipai-v1"` 改成 `v2`、`v3`，避免用户拿到旧缓存。
- 游戏源文件仍在 `中国象棋/` 和 `麻将/`，更新后记得重新复制到 `qipai/`。