# DESIGN.md — とーくる

> このファイルはAIエージェントが日本語UIを生成するためのデザイン仕様書です。
> ヒアリングデータを元にAIが自動生成します。手動編集も可能です。

---

## 0. Project Overview

- **ビジネス名**: とーくる
- **業種/ジャンル**: サービスプロモーション
- **目的**: 「とーくる」を売り込むためのLP
- **連絡先情報**: 電話番号 `07055494714` (CTAやフッターに必ず記載すること)

---

## 1. Visual Theme & Atmosphere

- **デザイン方針**: ダークモダン、先進的、ネオンアクセント
- **密度**: ゆったり（長文を避け、カード型で簡潔に）
- **キーワード**: 先進的、スタイリッシュ、ミニマル、インパクト

---

## 2. Color Palette & Roles

### Primary & Accents（ブランド＆ネオンカラー）

- **Primary (Cyan)** (`#00F0FF`): メインのブランドカラー。CTAボタン、リンク、主要なネオン発光に使用
- **Primary Dark** (`#00C2CC`): ホバー・プレス時
- **Accent (Pink)** (`#FF007F`): サブアクセント。バッジ、特記事項、セカンダリCTAのアクセント
- **Accent (Indigo)** (`#4F46E5`): 背景の微かなグラデーションやカードのボーダーハイライトに使用

### Semantic

- **Danger** (`#EF4444`): エラー、削除
- **Warning** (`#F59E0B`): 警告
- **Success** (`#10B981`): 成功、完了

### Neutral

- **Text Primary** (`#FAFAFA`): 本文テキスト
- **Text Secondary** (`#A3A3A3`): 補足テキスト
- **Border** (`#262626`): 区切り線、入力欄の枠
- **Background** (`#0A0A0A`): ページ背景
- **Surface / Card** (`#171717`): カード、モーダル等の面

---

## 3. Typography Rules

### 3.1 和文・欧文フォント指定

```css
font-family: "Inter", "Noto Sans JP", "Yu Gothic", system-ui, sans-serif;
```

### 3.2 文字サイズ・ウェイト階層

| Role | Size | Weight | Line Height | Letter Spacing |
|------|------|--------|-------------|----------------|
| Display | 48px | 700 | 1.2 | -0.02em |
| Heading 1 | 32px | 700 | 1.3 | -0.01em |
| Heading 2 | 24px | 600 | 1.4 | 0 |
| Heading 3 | 20px | 600 | 1.4 | 0 |
| Body | 16px | 400 | 1.7 | 0.04em |
| Caption | 14px | 400 | 1.5 | 0.04em |
| Small | 12px | 400 | 1.5 | 0.04em |

### 3.3 禁則処理・OpenType機能

- 本文: `word-break: break-all; overflow-wrap: break-word; line-break: strict;`
- 見出し・ナビゲーション: `font-feature-settings: "palt" 1, "kern" 1;`（字面を詰めてスタイリッシュに）

---

## 4. Component Stylings

### Buttons

**Primary**
- Background: Primary (`#00F0FF`)
- Text: `#0A0A0A`
- Padding: 12px 24px / Radius: 10px / Weight: 600
- Shadow: `0 0 20px rgba(0, 240, 255, 0.3)` (ネオングロウ)

**Secondary / Outline**
- Background: transparent
- Text: Primary (`#00F0FF`)
- Border: 1px solid Primary (`#00F0FF`)
- Padding: 12px 24px / Radius: 10px

### Cards

- Background: `#171717`
- Border: 1px solid `#262626`
- Border Radius: 12px
- Padding: 24px
- Shadow: `0 4px 20px rgba(0, 0, 0, 0.5)`

---

## 5. Layout & Spacing

- **Scale**: XS(8px), S(16px), M(24px), L(32px), XL(48px), XXL(80px)
- **Container**: Max Width 1200px, Padding 24px

---

## 6. Depth & Elevation (Shadows)

| Level | Shadow | 用途 |
|-------|--------|------|
| Card | `0 4px 20px rgba(0, 0, 0, 0.5)` | 通常のカード |
| Dropdown | `0 8px 30px rgba(0, 0, 0, 0.7)` | 浮き出る要素 |
| Neon Cyan | `0 0 20px rgba(0, 240, 255, 0.3)` | Primaryネオン発光 |
| Neon Pink | `0 0 20px rgba(255, 0, 127, 0.3)` | Accentネオン発光 |

---

## 7. Do's and Don'ts

### Do
- フォントフォールバック（Inter → Noto Sans JP）を徹底する
- ダークテーマに合わせたネオンカラーのアクセント（Cyan/Pink/Indigo）を効果的に使う
- 余白をしっかり取り、カード型で情報を整理する（長文を避ける）
- お問い合わせ導線に電話番号（`07055494714`）を明記する

### Don't
- 明るすぎる背景色や、純粋な `#000000` をテキストに使用すること
- ネオンカラーの多用（アクセントとして全体の10%未満に抑える）
- 均一なレイアウトの反復による単調なデザイン

---

## 8. Agent Prompt Guide

- globals.css の `@theme` に Color Palette と Shadows (ネオン) を定義する
- Tailwind v4 の記法に従う
- CTAボタンには `shadow-neon` を付与して先進感を演出する
- 見出しクラスには `font-feature-settings: "palt" 1;` を適用する