<script setup lang="ts">
type Platform = 'windows' | 'macos' | 'linux' | 'mobile' | 'unknown'

const platform = ref<Platform>('unknown')

const downloads = {
  windows: { label: '下載 Windows 版', href: 'https://github.com/llavon-ime/ime-windows/releases/tag/latest' },
  macos: { label: '查看 macOS 安裝步驟', href: 'https://github.com/llavon-ime/homebrew-llavon-ime#使用者安裝一鍵安裝' },
  linux: { label: '查看 Linux 安裝步驟', href: 'https://github.com/llavon-ime/ime-fcitx5#linux' }
} as const

const primaryDownload = computed(() => {
  if (platform.value === 'windows' || platform.value === 'macos' || platform.value === 'linux') {
    return downloads[platform.value]
  }
  return null
})

onMounted(() => {
  const userAgent = navigator.userAgent
  if (/Android|iPhone|iPad|iPod|Mobile|Tablet/i.test(userAgent)
    || (navigator.platform === 'MacIntel' && navigator.maxTouchPoints > 1)) {
    platform.value = 'mobile'
  } else if (/Windows/i.test(userAgent)) {
    platform.value = 'windows'
  } else if (/Macintosh|Mac OS X/i.test(userAgent)) {
    platform.value = 'macos'
  } else if (/CrOS/i.test(userAgent)) {
    platform.value = 'unknown'
  } else if (/Linux/i.test(userAgent)) {
    platform.value = 'linux'
  }
})

useSeoMeta({
  title: '拉風輸入法 — 本機語言模型注音輸入法',
  description: '拉風輸入法以大型語言模型（LLM）技術棧為核心，使用專為繁體中文注音訓練的模型，在本機根據前文與注音選字。',
  ogTitle: '拉風輸入法',
  ogDescription: '使用本機語言模型選字的繁體中文注音輸入法。',
  ogType: 'website',
  ogImage: '/llavon-avatar.png',
  twitterCard: 'summary'
})
</script>

<template>
  <div class="site-shell">
    <a class="skip-link" href="#top">跳至主要內容</a>
    <header class="site-header wrap">
      <a class="brand" href="#top" aria-label="拉風輸入法，回到頁首">
        <img class="brand-logo" src="/llavon-avatar.png" alt="" width="42" height="42">
        <span class="brand-name">拉風輸入法</span>
      </a>
      <nav class="header-nav" aria-label="主要導覽">
        <a href="#features">特色</a>
        <a href="#how-it-works">如何運作</a>
        <a href="#get-started">下載</a>
      </nav>
      <details class="mobile-nav">
        <summary aria-label="展開導覽選單"><span></span><span></span><span></span></summary>
        <nav aria-label="手機導覽">
          <a href="#features">特色</a>
          <a href="#how-it-works">如何運作</a>
          <a href="#get-started">下載</a>
        </nav>
      </details>
      <a class="header-github" href="https://github.com/llavon-ime" target="_blank" rel="noopener noreferrer" aria-label="在 GitHub 查看拉風輸入法（另開新分頁）">
        <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 .8a11.2 11.2 0 0 0-3.54 21.83c.56.1.77-.24.77-.54v-2.08c-3.12.68-3.78-1.32-3.78-1.32-.51-1.3-1.25-1.65-1.25-1.65-1.02-.7.08-.69.08-.69 1.13.08 1.73 1.16 1.73 1.16 1 .1 1.54.63 2.27.46.1-.73.39-1.23.71-1.51-2.49-.29-5.11-1.25-5.11-5.53 0-1.22.44-2.22 1.15-3-.12-.28-.5-1.42.11-2.96 0 0 .94-.3 3.08 1.15A10.7 10.7 0 0 1 12 5.27c.95 0 1.9.13 2.79.38 2.14-1.45 3.07-1.15 3.07-1.15.61 1.54.23 2.68.12 2.96.72.78 1.15 1.78 1.15 3 0 4.29-2.62 5.24-5.12 5.52.4.35.76 1.02.76 2.06v4.05c0 .3.2.65.77.54A11.2 11.2 0 0 0 12 .8Z"/></svg>
        <span>GitHub</span>
        <span class="arrow-up" aria-hidden="true">↗</span>
      </a>
    </header>

    <main id="top">
      <section class="hero wrap" aria-labelledby="hero-title">
        <div class="hero-copy">
          <div class="eyebrow"><span class="eyebrow-line"></span> 拉風輸入法 / 繁體中文注音輸入法</div>
          <h1 id="hero-title">使用語境選字的<br><em>注音輸入法</em></h1>
          <p class="hero-description">拉風輸入法以大型語言模型（LLM）技術棧為核心，使用專為繁體中文注音訓練的模型，根據前文、已選文字和注音預測候選字。推論在本機完成，輸入內容不需要送往雲端。</p>
          <p class="hero-distinction">本專案絕不是直接將現有大語言模型服務或現成模型接至注音輸入法。</p>
          <div class="hero-actions">
            <a v-if="primaryDownload" class="button button-primary" :href="primaryDownload.href" target="_blank" rel="noopener noreferrer">{{ primaryDownload.label }} <span aria-hidden="true">↗</span></a>
            <span v-else-if="platform === 'mobile'" class="button button-unavailable" role="status">手機端不支援</span>
            <a v-else class="button button-primary" href="#get-started">查看支援平台 <span aria-hidden="true">↓</span></a>
            <a class="button button-text" href="#get-started">查看各平台 <span aria-hidden="true">↓</span></a>
          </div>
          <p class="hero-note">Windows x64 · macOS arm64 · Linux x86_64　／　專案仍在開發中</p>
        </div>

        <div class="hero-visual" aria-label="本機選字流程示意">
          <div class="visual-orbit orbit-one" aria-hidden="true"></div>
          <div class="visual-orbit orbit-two" aria-hidden="true"></div>
          <div class="visual-accent" aria-hidden="true">ㄌ</div>
          <div class="visual-caption">L L A V O N　 /　 I M E</div>
          <div class="composition-card">
            <div class="card-topline"><span class="card-dots"><i></i><i></i><i></i></span><span>選字流程</span><span class="card-top-icon">✳</span></div>
            <div class="model-label">本機語言模型</div>
            <div class="model-name">2.5 億 <span>參數</span></div>
            <div class="model-description">GGUF 量化模型 · 在裝置上推論</div>
            <div class="model-flow">
              <div><small>輸入</small><span>前文 · 注音 · 已選文字</span></div>
              <div><small>約束</small><span>只保留讀音相符的候選</span></div>
              <div><small>選字</small><span>模型依語境排序</span></div>
            </div>
          </div>
          <div class="visual-footnote">本機處理 <span>—</span> 不上傳輸入內容</div>
        </div>
      </section>

      <section id="features" class="features-section section-pad">
        <div class="wrap">
          <div class="section-heading">
            <span class="section-index">01 / 特色</span>
            <h2>主要特色</h2>
          </div>
          <div class="features-grid">
            <article class="feature-item">
              <span class="feature-number">01</span>
              <div class="feature-symbol" aria-hidden="true">文<span>脈</span></div>
              <h3>依上下文選字</h3>
              <p>模型結合前文、注音序列與已選文字，預測適合目前句子的候選字。</p>
              <a class="feature-link" href="https://www.csie.ntpu.edu.tw/uploads/file/f1_202606101504240352.pdf" target="_blank" rel="noopener noreferrer">了解更多 ↗</a>
            </article>
            <article class="feature-item">
              <span class="feature-number">02</span>
              <div class="feature-symbol feature-symbol-phonetic" aria-hidden="true">ㄅ<span>ㄆ</span></div>
              <h3>專為注音訓練</h3>
              <p>使用繁體中文注音專用模型，並以合法注音候選集合約束預測結果。</p>
              <a class="feature-link" href="https://huggingface.co/tony65535/llavon-ime-llama-250m-GGUF" target="_blank" rel="noopener noreferrer">查看 Hugging Face 模型 ↗</a>
            </article>
            <article class="feature-item">
              <span class="feature-number">03</span>
              <div class="feature-symbol" aria-hidden="true">本<span>機</span></div>
              <h3>完全本機推論</h3>
              <p>模型在裝置上執行，輸入內容無須傳送至雲端，也能離線使用。</p>
              <a class="feature-link" href="https://github.com/ggml-org/llama.cpp" target="_blank" rel="noopener noreferrer">了解 llama.cpp ↗</a>
            </article>
            <article class="feature-item">
              <span class="feature-number">04</span>
              <div class="feature-symbol feature-symbol-lora" aria-hidden="true">LoRA</div>
              <h3>個人化 LoRA 微調</h3>
              <p>利用輸入紀錄在本機微調模型，讓選字更貼近你的用字習慣。訓練紀錄加密保存在本機。</p>
              <div class="feature-links">
                <a class="feature-link" href="https://github.com/llavon-ime/lora-trainer" target="_blank" rel="noopener noreferrer">了解 LoRA 微調 ↗</a>
                <a class="feature-link" href="https://zh-classical.wikipedia.org/wiki/%E5%85%AC%E9%91%B0%E5%82%B3%E5%AF%86%E8%A1%93" target="_blank" rel="noopener noreferrer">了解加密 ↗</a>
              </div>
            </article>
          </div>
        </div>
      </section>

      <section id="how-it-works" class="how-section section-pad">
        <div class="wrap how-layout">
          <div class="how-intro">
            <span class="section-index">02 / 運作方式</span>
            <h2>選字流程</h2>
            <p>輸入法前端與系統溝通並接收注音及呈現候選字；共用跨平台 C++ 核心載入模型以完成本地推論。</p>
            <a class="inline-link" href="https://github.com/llavon-ime/ime-core" target="_blank" rel="noopener noreferrer">查看 ime-core 原始碼 <span aria-hidden="true">↗</span></a>
          </div>
          <div class="flow-list" aria-label="輸入法運作流程">
            <div class="flow-item"><span class="flow-step">01</span><div><h3>接收輸入</h3><p>取得注音、已選文字與可用的前文。</p></div><span class="flow-glyph" aria-hidden="true">ㄅㄆ</span></div>
            <div class="flow-item"><span class="flow-step">02</span><div><h3>本機推論</h3><p>專用模型分析目前的輸入語境。</p></div><span class="flow-glyph" aria-hidden="true">···</span></div>
            <div class="flow-item"><span class="flow-step">03</span><div><h3>約束候選</h3><p>從讀音相符的字詞中選出預測結果。</p></div><span class="flow-glyph" aria-hidden="true">字</span></div>
          </div>
        </div>
      </section>

      <section id="get-started" class="get-section section-pad">
        <div class="wrap">
          <div class="get-heading"><div><span class="section-index">03 / 各平台</span><h2>下載與安裝</h2></div><p>各平台的安裝條件與步驟可能隨版本變動；請以專案 README 和發布頁為準。</p></div>
          <div class="platform-grid">
            <a class="platform-card" href="https://github.com/llavon-ime/ime-windows/releases/tag/latest" target="_blank" rel="noopener noreferrer">
              <span class="platform-meta">WINDOWS 10+ · X64 <span>↗</span></span>
              <span class="platform-title">Windows <span>↗</span></span>
              <span class="platform-desc">一般使用者下載最新發布頁面的 <code>*-setup.exe</code>；安裝程式會下載並驗證預設模型。</span>
              <span class="platform-end">前往下載頁 <span>→</span></span>
            </a>
            <a class="platform-card" href="https://github.com/llavon-ime/homebrew-llavon-ime#使用者安裝一鍵安裝" target="_blank" rel="noopener noreferrer">
              <span class="platform-meta">MACOS · ARM64 <span>↗</span></span>
              <span class="platform-title">macOS <span>↗</span></span>
              <span class="platform-desc">透過 Homebrew Cask 安裝原生輸入法。首次安裝後請在系統設定加入輸入方式，並登出再登入。</span>
              <span class="platform-end">查看安裝步驟 <span>→</span></span>
            </a>
            <a class="platform-card" href="https://github.com/llavon-ime/ime-fcitx5#linux" target="_blank" rel="noopener noreferrer">
              <span class="platform-meta">LINUX · X86_64 <span>↗</span></span>
              <span class="platform-title">Linux <span>↗</span></span>
              <span class="platform-desc">使用 Fcitx 5。提供原始碼建置與 x86_64 的 <code>.deb</code> / <code>.rpm</code> 套件；系統版本需求請看安裝說明。</span>
              <span class="platform-end">查看安裝步驟 <span>→</span></span>
            </a>
          </div>
          <div class="license-panel" aria-label="授權資訊">
            <div><span>程式碼</span><strong>BSD 2-Clause</strong><a href="https://github.com/llavon-ime/ime-windows/blob/main/LICENSE" target="_blank" rel="noopener noreferrer">查看授權 ↗</a></div>
            <div><span>公開模型權重</span><strong>CC BY-NC 4.0</strong><a href="https://huggingface.co/tony65535/llavon-ime-llama-250m-GGUF" target="_blank" rel="noopener noreferrer">查看模型授權 ↗</a></div>
          </div>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <div class="wrap footer-inner">
        <div><a class="footer-brand" href="#top">拉風輸入法</a><p>開源的繁體中文注音輸入法</p></div>
        <div class="footer-links"><a href="https://github.com/llavon-ime" target="_blank" rel="noopener noreferrer">GitHub ↗</a><a href="https://discord.gg/JCnFTW8K4P" target="_blank" rel="noopener noreferrer">Discord ↗</a><a href="https://github.com/llavon-ime/ime-windows/issues" target="_blank" rel="noopener noreferrer">Windows issue ↗</a><a href="https://github.com/llavon-ime/ime-fcitx5/issues" target="_blank" rel="noopener noreferrer">macOS / Linux issue ↗</a></div>
      </div>
      <div class="wrap footer-bottom"><span>© {{ new Date().getFullYear() }} Llavon IME</span><span>Windows · macOS · Linux</span></div>
    </footer>
  </div>
</template>
