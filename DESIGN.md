# DESIGN.md — {{サービス名}}

> このファイルはAIエージェントが日本語UIを生成するためのデザイン仕様書です。
> ヒアリングデータを元にAIが自動生成します。手動編集も可能です。

---

## 1. Visual Theme & Atmosphere

- **デザイン方針**: {{AIが業種から判断}}
- **密度**: {{ゆったり / 標準 / 情報密度高め}}
- **キーワード**: {{3〜5つの形容詞}}

---

## 2. Color Palette & Roles

### Primary（ブランドカラー）

- **Primary** (`#______`): メインのブランドカラー。CTAボタン、リンク等に使用
- **Primary Dark** (`#______`): ホバー・プレス時

### Semantic

- **Danger** (`#EF4444`): エラー、削除
- **Warning** (`#F59E0B`): 警告
- **Success** (`#10B981`): 成功、完了

### Neutral

- **Text Primary** (`#171717`): 本文テキスト
- **Text Secondary** (`#737373`): 補足テキスト
- **Border** (`#E5E5E5`): 区切り線、入力欄の枠
- **Background** (`#FAFAFA`): ページ背景
- **Surface** (`#FFFFFF`): カード、モーダル等の面

---

## 3. Typography Rules

### 3.1 和文フォント

- **ゴシック体**: Noto Sans JP, 游ゴシック体, "Yu Gothic", sans-serif

### 3.2 欧文フォント

- **サンセリフ**: Inter, -apple-system, system-ui, sans-serif

### 3.3 font-family 指定

```css
font-family: "Inter", "Noto Sans JP", "Yu Gothic", system-ui, sans-serif;
```

### 3.4 文字サイズ・ウェイト階層

| Role | Size | Weight | Line Height | Letter Spacing |
|------|------|--------|-------------|----------------|
| Display | 48px | 700 | 1.2 | -0.02em |
| Heading 1 | 32px | 700 | 1.3 | -0.01em |
| Heading 2 | 24px | 600 | 1.4 | 0 |
| Heading 3 | 20px | 600 | 1.4 | 0 |
| Body | 16px | 400 | 1.7 | 0.04em |
| Caption | 14px | 400 | 1.5 | 0.04em |
| Small | 12px | 400 | 1.5 | 0.04em |

### 3.5 行間・字間

- 本文の行間: 1.7
- 見出しの行間: 1.3
- 本文の字間: 0.04em
- 見出しの字間: 0〜-0.02em

### 3.6 禁則処理

```css
word-break: break-all;
overflow-wrap: break-word;
line-break: strict;
```

### 3.7 OpenType 機能

```css
font-feature-settings: "palt" 1, "kern" 1;
```

見出し・ナビゲーションに palt 適用。本文は未適用。

---

## 4. Component Stylings

### Buttons

**Primary**
- Background: Primary カラー
- Text: #FFFFFF
- Padding: 12px 24px
- Border Radius: 10px
- Font Size: 16px / Weight: 600

**Secondary**
- Background: transparent
- Text: Primary カラー
- Border: 1px solid Primary
- Padding: 12px 24px
- Border Radius: 10px

### Inputs

- Border: 1px solid #E5E5E5
- Border (focus): 1px solid Primary
- Border Radius: 10px
- Padding: 12px 16px
- Height: 44px

### Cards

- Background: #FFFFFF
- Border: 1px solid #E5E5E5
- Border Radius: 12px
- Padding: 24px
- Shadow: 0 1px 2px rgba(0,0,0,0.05)

---

## 5. Layout Principles

### Spacing Scale

| Token | Value |
|-------|-------|
| XS | 8px |
| S | 16px |
| M | 24px |
| L | 32px |
| XL | 48px |
| XXL | 80px |

### Container

- Max Width: 1200px
- Padding: 24px

---

## 6. Depth & Elevation

| Level | Shadow | 用途 |
|-------|--------|------|
| 0 | none | フラット |
| 1 | 0 1px 2px rgba(0,0,0,0.05) | カード |
| 2 | 0 4px 8px rgba(0,0,0,0.08) | ドロップダウン |
| 3 | 0 8px 24px rgba(0,0,0,0.12) | モーダル |

---

## 7. Do's and Don'ts

### Do

- フォントは必ずフォールバックチェーンを指定する
- 日本語本文の line-height は 1.5 以上
- コントラスト比 WCAG AA 以上を確保
- 余白は Spacing Scale に従う
- セクションごとにレイアウトに変化をつける

### Don't

- グラデーション背景の多用
- 装飾的なSVGパターン
- 全セクション同じレイアウトの繰り返し
- 不自然に大きなpadding
- 過剰なアニメーション
- 純粋な #000000 をテキストに使用

---

## 8. Responsive Behavior

| Name | Width | 説明 |
|------|-------|------|
| Mobile | ≤ 640px | 1カラム |
| Tablet | ≤ 1024px | 2カラム |
| Desktop | > 1024px | 2-3カラム |

- タッチターゲット最小: 44px × 44px
- モバイルでは見出しをデスクトップの 70-80% に縮小

---

## 9. Agent Prompt Guide

DESIGN.md を読んだ上で、以下のルールに従ってコードを生成すること:

- globals.css の CSS変数を Color Palette に合わせて更新する
- コンポーネントは shadcn/ui をベースにカスタマイズする
- Tailwind のユーティリティクラスを使い、インラインスタイルは使わない
- 画像は public/images/ に配置し、next/image の Image コンポーネントで表示する
- レスポンシブはモバイルファーストで記述する（sm:, md:, lg: の順）
