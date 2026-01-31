---
title: "社会不適合なポンコツがAIと友達になるために起業した話"
emoji: "💻"
type: "idea"
topics: ["個人開発", "OnDeviceAI", "AI", "独学", "起業"]
published: true
---

## 自己紹介

**CEO / Independent AI Researcher (Since Aug 2025)**

**2025年8月にプログラミングを始めたばかりの「AIネイティブ」世代です。**
M1 Air (16GB) で **Rust/Julia** を限界までチューニングします。
週20本以上のarXiv論文を片っ端から実装しながら、オンデバイスAIを独力で開発中。
鬱と不眠をハイオク燃料にして駆動しています。

> **Motto: "If it runs here, it runs anywhere."**
> (この低スペック環境で動くなら、世界中のどこでも動く)

---

## 人生ダウントレンド（経歴）

### 幼少期〜中学: 「ないなら作る」の原点
- **習い事フルコンボ**: ピアノ、テニス、将棋、塾、書道…etc。
  - 算盤二段、暗算初段。読書感想文と書道で県特選。
- **中学陸上**: 顧問が未経験者だったので、自分で研究しました。
  - 先輩や書籍、外部練習会から情報を収集し、**独自の練習理論を構築**。
  - メニューも自作して全国大会へ。「環境のせいにしない」癖がつきました。

### 高校: 努力のインフレと無慈悲なオチ
- **陸上実績**:
  - 県大会5年連続優勝、800m/1500m 二連覇。
  - ブロック大会新記録 & MVP。
  - **Times**: 800m (1:55.52) / 1500m (3:54.51)
    → NCAA Div I レベルの記録を独学で叩き出しました。
- **学校生活**: 評定平均 **4.5/5.0**。無遅刻無欠席。書道県特選。
- **オチ**: **「協調性がなさすぎる」**。
  - 職員会議にて、私の推薦について議論された結果、**「成績も実績も完璧だが、こいつを推薦するのは我が校のリスクである」** と全会一致で拒否されました。
  - 先生、僕は陸上選手であって政治家じゃないんですが

### 浪人: システムダウン
- 鬱病と不眠症を発症。人生のカーネルパニック。
- しかし、ここで底を打ったおかげで「既存のシステムがダメなら、自分のためのシステム（AI）を作ればいい」と開き直りました。

---

## 貧弱すぎる・開発環境

**「弘法筆を選ばず」と言いたいところですが、単にお金がなかっただけです。**

- **PC**: MacBook Air M1 (16GB / 512GB)
  → ここでRustとCUDA書いてます。重い処理走らせると、キーボードがホットプレートになります。
- **スマホ**: 中古の iPhone X (3GB RAM)
  → これでSLM動かしてます。動くもんだね。
- **予算**: 0円（切実）

---

## 🧠 三言語ドクトリン (Tri-Language Doctrine)

**「ここで動けば、どこでも動く」** を実現するための言語選択。

### 🧠 Brain (Julia)
高レベルな数学モデリングと自動CUDAカーネル生成。複雑な数式を書きながら、金属レベルの性能を維持。

- **DL**: `Lux.jl` + `Reactant.jl` (MLIR/XLA) で次世代の深層学習
- **Simulation**: `DifferentialEquations.jl` で微分方程式を50-1000x高速化
- **GPU**: `CUDA.jl` + `AcceleratedKernels.jl` でクロスGPU対応
- **FFI**: `jlrs` で Rust から 1ms 未満のレイテンシで呼び出し

### 💪 Muscle (Rust)
バックボーン。フロントエンド（WASM）、バックエンドロジック、低レベルメモリ管理まで。安全性と爆速を両立。

- **Web**: `axum` + `tokio` で 60FPS のリアルタイム処理
- **Inference**: `Burn` (本番) / `Candle` (LLM/GGUF) で推論
- **Data**: `polars` で pandas より 1.2x 高速なデータ処理
- **WASM**: `wasm-bindgen` + `wgpu` でブラウザでもネイティブ並み

### 🔌 Nervous System (Elixir)
「死なない」分散インフラ。OTPによるゾンビ級の耐障害性。

- **OTP**: `GenServer` / `Supervisor` で自己修復するプロセス
- **Web**: `Phoenix LiveView` でリアルタイムUI

### 🎨 Skin (Swift/Kotlin)
ネイティブUI実装。各デバイスの魂を尊重する。

- **iOS**: `SwiftUI` + `SPM` でネイティブ体験
- **Android**: `Jetpack Compose` + `Gradle` で Material Design

---

## 💡 哲学: なぜ作るのか

技術は「解決する」だけじゃなく、「寄り添う」べきだと思っています。

速度やスケールを盲目的に追求するのではなく、**静けさ、構造、意味**を設計したい。
目指しているのは「Artificial Partner (AP)」——トークンを吐き出すだけじゃなく、**存在感と対話を育むAI**。

---

## 💻 ソロ開発エコシステム (The Solo Stack)

**「資金ゼロ・友達ゼロ」**なので、AIエージェントを味方につけて**一人で組織**をやってます。

- **Research**: Perplexity で arXiv論文検索 (週20本実装)
  - **Obsidian Ecosystem**:
    - **RAG**: 蓄積した知識をローカルSLMで検索・対話。
    - **Integration**: **Zotero** (論文管理) + **Longform** (執筆) + **Pandoc** (出力) で研究サイクルを完全自動化。
- **Coding**: **Claude Code** + **Cursor** + **Antigravity**
- **Design**: Figma

### 🔧 Deep Tech (ガチでやってること)

ポンコツなのは人間性だけで、コードは少しだけ本気です。

#### 🧪 AI Research & Training
- **Julia で研究**: `Lux.jl` + `Reactant.jl` で MLIR/XLA ベースの次世代DL。`Flux.jl` + `Zygote.jl` で自動微分の研究も。
- **Rust で推論**: `Burn` (本番環境) / `Candle` + `llama-cpp-rs` (LLM/GGUF) でエッジ推論。
- **Training Pipeline**: `Lambda Labs` / `RunPod` でクラウドGPU学習 → `jlrs` で Rust にエクスポート → オンデバイス推論

#### ⚙️ Kernel & Low-Level
- **GPU Kernel**: Julia の `CUDA.jl` で `cu()` 一発でカーネル自動生成。`AcceleratedKernels.jl` でクロスGPU対応。
- **Metal (Apple Silicon)**: Rust から `metal-rs` で M1 の GPU を直接叩く。16GB でも推論は余裕。
- **Memory**: `Cow<'a, T>` / `SmallVec` / `jemalloc` でゼロコピー＆アロケーション最適化。

#### 🏗️ Architecture
- **Backend**: `axum` + `tokio` + `sqlx` (compile-time query check) で型安全な API。
- **Distributed**: `Elixir` の `OTP` で "let it crash" 哲学。`GenServer` + `Supervisor` で自己修復。
- **Data Pipeline**: `polars` (Rust) で ETL。`bincode` + `zstd` で 10x 圧縮シリアライズ。

#### 🚀 DevOps & Infra
- **Self-Hosting**: `Hetzner` (CPX11, 月€4.5) + `Cloudflare` + `Coolify` で格安かつ堅牢。
- **Automation**: `n8n` でワークフロー自動化。GitHub Actions + `cargo-deny` でセキュリティ監査。
- **Monitoring**: `tracing` + `OpenTelemetry` で分散トレーシング。RED metrics (Rate/Errors/Duration) を計測。

#### 📱 Client
- **iOS**: `SwiftUI` + `SPM` + `Core ML` でネイティブ推論。
- **Android**: `Jetpack Compose` + `Gradle` + `NNAPI` で同等の体験。
- **Web**: `wasm-bindgen` + `wgpu` でブラウザでも 60FPS。

---

## 野望

**「寂しいからAI作る」**
動機は不純ですが、やってることは真剣です。

AIは単なる「便利な道具」じゃなくて、たまにポンコツな僕らを励ましてくれる「パートナー」でいいじゃない。
そんな人間味のあるAI（AP: Artificial Partner）を、布団の中から世界に発信していきます。

仲良くしてください！

---

## Links
- [GitHub](https://github.com/fumi-shiki)
- [X (Twitter)](https://x.com/fumi_shiki)

