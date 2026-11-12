
# VS GUIDE 攻略ディレクトリ（Astro実装コード）

公式リポジトリ（`vampire-survivors-wiki/website`）のアーキテクチャおよび既存のコンポーネント構成（`Layout.astro`, `Header.astro`, `Footer.astro`, `global.css`）に完全準拠したコード一式です。

---

## ディレクトリ構成

```text
src/
├── pages/
│   └── strategy/
│       └── index.astro          # 攻略ディレクトリページ（PC / スマホ切り替え）
└── components/
    └── strategy/
        ├── StrategyDesktop.astro # 選択画面 ①: PC版・画像ハブUI
        └── StrategyMobile.astro  # 選択画面 ②: スマホ専用ビジュアルバナーUI
```

---

## 1. ページエントリー: `src/pages/strategy/index.astro`

`src/pages/index.astro` と同一のレスポンシブ切り替え設計です。

```astro
---
import Layout from '../../layouts/Layout.astro';
import StrategyDesktop from '../../components/strategy/StrategyDesktop.astro';
import StrategyMobile from '../../components/strategy/StrategyMobile.astro';
---

<Layout
  title="攻略ディレクトリ | VS GUIDE"
  description="Vampire Survivorsの攻略ディレクトリ。ステージ攻略、ボス攻略、キャラクター情報、アンロック攻略の各一覧への案内ハブです。"
  currentPath="/strategy/"
>
  <!-- PC画面 (md以上で表示) -->
  <div class="hidden md:block">
    <StrategyDesktop />
  </div>

  <!-- スマホ画面 (md未満で表示) -->
  <div class="block md:hidden">
    <StrategyMobile />
  </div>
</Layout>
```

---

## 2. PC版コンポーネント: `src/components/strategy/StrategyDesktop.astro`

UI画面：**攻略ディレクトリ - VS GUIDE (公式リポジトリ完全準拠・画像ハブ版)**

```astro
---
interface CategoryItem {
  id: string;
  number: string;
  label: string;
  title: string;
  description: string;
  href: string;
  ctaText: string;
  iconPath: string;
  subLabel: string;
}

const categories: CategoryItem[] = [
  {
    id: 'stages',
    number: '01',
    label: 'STAGES DIRECTORY',
    title: 'ステージ攻略',
    description: '本編・DLC全ステージのマップ構造、レリック回収ルート、推奨ビルドおよび生存手順の一覧です。',
    href: '/strategy/stages/',
    ctaText: '一覧を見る →',
    subLabel: 'STAGES & MAPS',
    iconPath: 'M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253',
  },
  {
    id: 'bosses',
    number: '02',
    label: 'BOSS MECHANICS',
    title: 'ボス攻略',
    description: '30分死神討伐手順、ディレクター等の最終ボスギミック対策、ステージ中ボスの弱点一覧です。',
    href: '/strategy/bosses/',
    ctaText: '一覧を見る →',
    subLabel: 'BOSSES & MECHANICS',
    iconPath: 'M14.121 14.121L19 19m-7-7l7-7m-7 7l-2.879 2.879a3 3 0 11-4.242-4.242L10.757 7.757m0 0L7.757 4.757a3 3 0 00-4.242 4.242l2.879 2.879',
  },
  {
    id: 'characters',
    number: '03',
    label: 'CHARACTER ARCHIVE',
    title: 'キャラクター情報',
    description: '通常・隠し・DLCキャラクターの初期武器、隠しパッシブ効果、解放条件や成長傾向の一覧です。',
    href: '/characters/',
    ctaText: '一覧を見る →',
    subLabel: 'SURVIVORS ARCHIVE',
    iconPath: 'M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z',
  },
  {
    id: 'secrets',
    number: '04',
    label: 'SECRETS & UNLOCKS',
    title: 'アンロック攻略',
    description: 'アチーブメント達成ルート、重要レリック獲得手順、隠し呪文コード（Spells）の一覧です。',
    href: '/strategy/unlocks/',
    ctaText: '一覧を見る →',
    subLabel: 'CIPHERS & SECRETS',
    iconPath: 'M15 7a2 2 0 012 2m4 0a6 6 0 01-7.743 5.743L11 17H9v2H7v2H4a1 1 0 01-1-1v-2.586a1 1 0 01.293-.707l5.964-5.964A6 6 0 1121 9z',
  },
];
---

<div class="w-full" data-posthog-page="strategy-directory" data-posthog-layout="desktop">
  <!-- ヒーローフロストガラス帯 -->
  <section class="w-full hero-glass-band pt-12 pb-8 mb-10" data-posthog-home-section="intro">
    <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8">
      <span class="text-xs font-mono font-medium tracking-widest text-slate-500 uppercase block mb-2">
        ARCHIVE & VERIFICATION COMPENDIUM
      </span>
      <h1 class="text-4xl lg:text-5xl font-extrabold tracking-tight text-slate-950 mb-3">
        攻略ディレクトリ
      </h1>
      <p class="text-sm text-slate-600 max-w-2xl leading-relaxed">
        ステージ攻略、ボス攻略、キャラクター情報、アンロック攻略の各一覧への案内ハブです。確認したい項目を選択してください。
      </p>

      <!-- アンカーショートカット -->
      <div class="flex items-center gap-6 mt-6 text-xs font-mono text-slate-500">
        {categories.map((cat) => (
          <a
            href={`#${cat.id}`}
            class="hover:text-slate-900 transition-colors"
          >
            {cat.number} {cat.title.replace('情報', '').replace('攻略', '')} ↓
          </a>
        ))}
      </div>
    </div>
  </section>

  <!-- メインリスト（画像ハブカード） -->
  <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 pb-16">
    <div class="space-y-6">
      {categories.map((item) => (
        <section
          id={item.id}
          class="glass-panel rounded-2xl overflow-hidden p-6 lg:p-8 flex flex-col md:flex-row items-center gap-8 transition-all hover:shadow-md"
        >
          <!-- 左側：画像プレースホルダー枠 -->
          <div class="w-full md:w-[380px] lg:w-[440px] h-[210px] rounded-xl bg-slate-100/90 border border-slate-200/60 flex flex-col items-center justify-center text-center p-6 shrink-0 group">
            <div class="w-12 h-12 rounded-xl bg-white/80 border border-slate-200/80 flex items-center justify-center text-blue-600 shadow-xs mb-3 group-hover:scale-105 transition-transform">
              <svg class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.75">
                <path stroke-linecap="round" stroke-linejoin="round" d={item.iconPath} />
              </svg>
            </div>
            <span class="text-xs font-mono font-bold tracking-widest text-slate-600 uppercase">
              {item.subLabel}
            </span>
          </div>

          <!-- 右側：コンテンツ詳細＆右寄せCTA -->
          <div class="flex-1 flex flex-col justify-between h-full w-full py-1">
            <div>
              <div class="flex items-center gap-2 mb-2">
                <span class="text-xs font-mono font-bold text-blue-600">
                  {item.number} {item.label}
                </span>
              </div>
              <h2 class="text-2xl font-extrabold tracking-tight text-slate-950 mb-3">
                {item.title}
              </h2>
              <p class="text-sm text-slate-600 leading-relaxed max-w-2xl">
                {item.description}
              </p>
            </div>

            <!-- 右端寄せのCTAリンクボタン -->
            <div class="flex justify-end pt-6 mt-4 border-t border-slate-200/50">
              <a
                href={item.href}
                class="inline-flex items-center gap-2 px-5 py-2.5 rounded-xl bg-slate-950 text-white text-xs font-bold hover:bg-slate-800 transition-colors shadow-xs group"
              >
                <span>{item.ctaText}</span>
              </a>
            </div>
          </div>
        </section>
      ))}
    </div>
  </div>
</div>
```

---

## 3. スマホ版コンポーネント: `src/components/strategy/StrategyMobile.astro`

UI画面：**攻略ディレクトリ - VS GUIDE (スマホ専用ビジュアルバナーUI)**

```astro
---
interface MobileBannerItem {
  number: string;
  categoryTag: string;
  title: string;
  description: string;
  href: string;
  bgGradient: string;
  imageSrc?: string;
}

const bannerItems: MobileBannerItem[] = [
  {
    number: '01',
    categoryTag: 'STAGES',
    title: 'ステージ攻略',
    description: '本編・DLC全マップ構造と生存手順',
    href: '/strategy/stages/',
    bgGradient: 'from-slate-950/90 via-slate-900/80 to-slate-950/95',
  },
  {
    number: '02',
    categoryTag: 'BOSSES',
    title: 'ボス攻略',
    description: '死神撃破・ギミックボスの行動パターン',
    href: '/strategy/bosses/',
    bgGradient: 'from-slate-950/90 via-red-950/70 to-slate-950/95',
  },
  {
    number: '03',
    categoryTag: 'CHARACTERS',
    title: 'キャラクター情報',
    description: '通常・隠し・DLCキャラクターの性能と固有能力',
    href: '/characters/',
    bgGradient: 'from-slate-950/90 via-blue-950/70 to-slate-950/95',
  },
  {
    number: '04',
    categoryTag: 'SECRETS',
    title: 'アンロック攻略',
    description: 'アチーブメント達成・モーベインの秘密の呪文…',
    href: '/strategy/unlocks/',
    bgGradient: 'from-slate-950/90 via-amber-950/70 to-slate-950/95',
  },
];
---

<div class="px-4 py-6 space-y-5" data-posthog-page="strategy-directory" data-posthog-layout="mobile">
  <!-- スマホパンくず & タイトル -->
  <div class="space-y-1.5">
    <div class="flex items-center gap-1.5 text-[11px] font-medium text-slate-500">
      <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
      </svg>
      <a href="/" class="hover:text-slate-900">ホーム</a>
      <span>/</span>
      <span class="text-slate-900 font-bold">攻略</span>
    </div>

    <h1 class="text-2xl font-extrabold tracking-tight text-slate-950">
      攻略ディレクトリ
    </h1>
    <p class="text-xs text-slate-600 leading-relaxed">
      確認したい攻略カテゴリーを選択してください。各一覧へ移動します。
    </p>
  </div>

  <!-- スマホ専用ビジュアルバナーリスト -->
  <div class="space-y-3.5 pt-1">
    {bannerItems.map((banner) => (
      <a
        href={banner.href}
        class="relative block w-full rounded-2xl overflow-hidden shadow-xs border border-slate-200/80 active:scale-[0.98] transition-transform duration-200"
      >
        <!-- 背景ビジュアル領域（ダークグラデーション＋テクスチャ） -->
        <div class={`w-full min-h-[148px] p-5 flex items-center justify-between bg-gradient-to-r ${banner.bgGradient} relative`}>
          <!-- ドット/ノイズオーバーレイ -->
          <div class="absolute inset-0 bg-[radial-gradient(#ffffff_1px,transparent_1px)] [background-size:16px_16px] opacity-10"></div>

          <!-- バナー情報（左側） -->
          <div class="relative z-10 flex-1 pr-4 space-y-1">
            <div class="inline-flex items-center gap-1.5 px-2 py-0.5 rounded-md bg-white/10 backdrop-blur-xs border border-white/15 text-[10px] font-mono font-bold tracking-wider text-slate-200">
              <span>{banner.number} {banner.categoryTag}</span>
            </div>
            <h2 class="text-lg font-bold text-white tracking-tight pt-0.5">
              {banner.title}
            </h2>
            <p class="text-[11px] text-slate-300 leading-snug line-clamp-1">
              {banner.description}
            </p>
          </div>

          <!-- 親指操作用大型円形CTAボタン（右側） -->
          <div class="relative z-10 w-11 h-11 rounded-full bg-white text-slate-950 flex items-center justify-center shrink-0 shadow-md">
            <svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M14 5l7 7m0 0l-7 7m7-7H3" />
            </svg>
          </div>
        </div>
      </a>
    ))}
  </div>
</div>
```