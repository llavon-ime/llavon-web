# Llavon IME 網站

拉風輸入法的網站，使用 Nuxt 4 製作。網站內容依據 [組織介紹](https://github.com/llavon-ime/.github)、[Windows 版](https://github.com/llavon-ime/ime-windows)、[Unix 版](https://github.com/llavon-ime/ime-fcitx5)、[Homebrew Tap](https://github.com/llavon-ime/homebrew-llavon-ime) 與 [推論核心](https://github.com/llavon-ime/ime-core) 的原始碼和 README 撰寫。

## 開發

需要 Node.js 22 或更新版本。

```bash
npm install
npm run dev
```

開啟 `http://localhost:3000`。

## 建置

```bash
npm run build
npm run generate
```

`generate` 會產生可部署到靜態網站主機的 `.output/public`。

Windows 按鈕連至最新發布頁；macOS 和 Linux 按鈕連至各平台的安裝說明。平台支援與安裝方式可能變動，更新網站時請先核對各儲存庫的 README。
