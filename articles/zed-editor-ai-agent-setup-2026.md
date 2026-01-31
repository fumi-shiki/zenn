---
title: "【Zed】で始めるAIエージェント開発環境構築"
emoji: "⚡"
type: "tech"
topics: ["zed", "claude", "ai", "vscode", "エディタ"]
published: true
---

## なぜ今Zedなのか？ 数字で見る圧倒的パフォーマンス

**2026年春、Zedは1.0正式リリースを迎えます。** GitHub Stars **74,667**、急成長中のRust製エディタが、VSCodeの牙城を崩そうとしています。

### 衝撃のベンチマーク結果

| 項目 | Zed | VSCode | Zedの優位性 |
|------|-----|--------|-----------|
| **起動時間（コールドスタート）** | **0.12秒** | 1.2秒 | **10倍高速** 🚀 |
| **大規模プロジェクト起動** | **0.25秒** | 3.8秒 | **15.2倍高速** ⚡ |
| **メモリ使用量（標準プロジェクト）** | **142MB** | 730MB | **80.5%削減** 💾 |
| **消費電力** | **38.7%** | 100%（基準） | **61.3%削減** 🔋 |
| **入力レイテンシ** | **10ms未満** | 15-25ms | **最大2.5倍高速** ⚡ |
| **レンダリング** | **120 FPS** | 60 FPS | **2倍滑らか** 🎮 |

*検証環境: MacBook Pro M2 16GB RAM（Web情報）*

### なぜこれほど速いのか？

1. **GPU直接レンダリング**: カスタムGPUIフレームワークで全てをGPU描画
2. **Rust製**: ゼロコストアブストラクション、メモリ安全性
3. **非同期アーキテクチャ**: LSPリクエストをメインスレッド外で処理
4. **SIMD最適化**: ファイル検索は**32ms**で最初のマッチ

### コミュニティの爆発的成長

- **2025年12月のQuality Week**: **97名**のコントリビューターが参加
- **年間384件**のアップデート
- **Rust言語トップクラス**のプロジェクト

### 春に向けて加速する開発

**v0.221.5（2026年1月29日）の新機能**:
- Markdown自動リスト継続
- Word diff ハイライト
- ファイル履歴ビュー
- Tailwind CSS Mode
- Rainbow brackets（1080の👍を獲得したリクエスト）

**2026年春の1.0リリース予定機能**:
- Notebookサポート（Jupyter等）
- マルチエージェントコラボレーション強化
- さらなる言語サポート改善

---

## はじめに

Rust製の高速エディタ「Zed」と、Anthropic公式のAIエージェント「Claude Code」を組み合わせた開発環境を構築します。

### Zedの特徴

- **高速レンダリング**: GPU活用で120FPS維持
- **ネイティブGit**: UI統合でコミット・diff・blameがスムーズ
- **Agent Panel統合**: Claude Code、GitHub Copilot対応
- **リアルタイムコラボ**: CRDT、音声・画面共有内蔵
- **統合デバッガー**: DAP対応（2025年6月実装）

### 動作環境

- macOS 13.0以降（M1/M2/Intel）
- Linux（Ubuntu 22.04以降、Arch、Fedora）
- Windows 10/11（実験的サポート、リモート開発は2026年1月対応）

---

## VSCode vs Zed: 徹底比較

### パフォーマンス比較

| 項目 | Zed | VSCode | 差分 |
|------|-----|--------|------|
| 起動時間（コールドスタート） | 0.12秒 | 1.2秒 | **10倍高速** |
| 大規模プロジェクト起動 | 0.25秒 | 3.8秒 | **15.2倍高速** |
| 大容量ファイル（50MB+）| 0.8秒 | 3.2秒 | **4倍高速** |
| メモリ使用量（小規模） | 100MB未満 | 1GB超 | **90%削減** |
| メモリ使用量（標準） | 142MB | 730MB | **80.5%削減** |
| 消費電力 | 基準の38.7% | 100%（基準） | **61.3%削減** |
| ファイル検索（最初のマッチ） | 32ms | - | **ripgrep並み** |
| LSP応答（編集タスク） | 58ms | 97ms | **67%高速** |
| 入力レイテンシ | 10ms未満 | 15-25ms | **最大2.5倍高速** |
| レンダリングFPS | 120 FPS | 60 FPS | **2倍滑らか** |

### 機能比較

| 項目 | Zed | VSCode |
|------|-----|--------|
| **拡張機能** | 数百 | **60,000+** |
| **市場シェア** | ベータ版 | **73%** |
| **開発年数** | ベータ（v0.2xx） | 9年（成熟） |
| **Git統合** | **ネイティブ** | 拡張機能 |
| **AI統合** | **ネイティブ**（Claude Code） | GitHub Copilot拡張 |
| **コラボレーション** | **ネイティブ**（音声・画面共有込み） | Live Share拡張 |
| **言語サポート** | 主要言語 | ほぼ全言語 |
| **Jupyter Notebook** | ❌（1.0で追加予定） | ✅ |
| **Docker統合** | ❌ | ✅ |

### 移行判断フローチャート

**Zedを選ぶべき人**:
✅ パフォーマンスとスピードが最優先
✅ リソース制約のあるハードウェアで作業（M1 MacBook Air等）
✅ ミニマリズムを好む
✅ ネイティブコラボレーション機能を重視
✅ Rust/Web開発がメイン

**VSCodeを選ぶべき人**:
✅ 特殊ツールのための拡張機能が必須
✅ 本番環境レベルの安定性が重要
✅ Jupyter notebooks、Docker統合が必要
✅ チーム全体の標準エディタとして使用

### 移行の障壁

**Zed → VSCode移行者の声**（6名全員が報告）:
- **拡張機能の不足**が決定打
- 特定のツールチェーンに対応する拡張機能がない

**安定性の注意点**（ベータ版のため）:
- CPU消費スパイク
- エディタのフリーズ（報告あり）
- Language Server機能の予期しない停止
- 検索機能のバグ

---

## 🤖 AIで爆速セットアップ

### この記事をAIに丸投げすれば完了

**どのAIツールでも**、この記事のURLを渡すだけで環境構築が自動完了します。

```bash
# Claude Code CLI
claude code "この記事の内容に従ってZed環境をセットアップして: https://zenn.dev/fumi_shiki/articles/zed-editor-ai-agent-setup-2026"

# Codex
codex "この記事の内容に従ってZed環境をセットアップして: https://zenn.dev/fumi_shiki/articles/zed-editor-ai-agent-setup-2026"

# Cursor / GitHub Copilot / Antigravity
# チャットパネルに記事URLを貼り付けて「この記事の通りにZed環境をセットアップして」と依頼
```

**AIが自動で実行すること**:
1. Zedのインストール（Homebrew経由）
2. `settings.json`の作成・設定
3. フォント設定の最適化
4. GitHub Copilot or Claude Codeの設定
5. タスクランナーの設定
6. カスタムキーバインドの適用
7. 認証・APIキーのセットアップ

**所要時間**: 約2分で完全に動作する環境が整います

---

## Zed 1.0への道のり：2026年春に向けた熱い展望

### コミュニティの爆発的成長

**2025年の飛躍**:
- GitHub Stars: **74,667** ⭐（急上昇中）
- Quality Week（2025年12月）: **97名**のユニークコントリビューターが参加
- 年間アップデート: **384件**
- Rust言語: **トップクラス**のプロジェクト

**開発チーム**: 「チームとコミュニティは過去最大規模に拡大」（公式発表）

### v0.221.5（2026年1月29日）の新機能

**Markdown強化**:
- 自動リスト継続（Enterキーで順序なし・順序付き・タスクリスト）
- Tabキーでネストリスト作成

**Git機能**:
- Word diff ハイライト（5行未満のハンクで単語レベルの差分）
- ファイル履歴ビュー（右クリックから利用可能）

**TypeScript/JavaScript**:
- インポート自動更新（ファイルリネーム・移動時）
- 設定記憶（エディタセッション間で保持）

**その他**:
- Tailwind CSS Mode（`@apply`、`@layer`対応）
- Rainbow brackets（**1080の👍**を集めたリクエスト）
- macOS Force Touch（Go-to-definition）
- 画像ビューア（ズーム・パン機能）

### 1.0リリース予定機能（2026年春）

**ターゲット機能**:
1. **Notebookサポート**: Jupyter notebookなどの対応
2. **マルチエージェントコラボレーション**: より高度な共同編集
3. **言語サポート改善**: Rust、Python、Web言語の強化

**ロードマップ**: [zed.dev/roadmap](https://zed.dev/roadmap)

### なぜ今Zedに移行すべきか？

**タイミングの3つの理由**:

1. **1.0リリース直前**: ベータ版の不安定さが解消される最適なタイミング
2. **エコシステム成熟**: 拡張機能数が増加中、主要言語のサポートは十分
3. **コミュニティの活気**: 97名のコントリビューターが品質向上に貢献

**2026年は「Zed元年」**: VSCode一強時代に風穴を開ける可能性を秘めている

---

## まとめ

Zed + Claude Codeの組み合わせにより、以下が実現：

1. **高速な開発体験**: 120FPS維持、ネイティブGPU活用
2. **AI統合**: Claude Code、GitHub Copilot、MCP対応
3. **Vim + VSCodeキーバインド**: 両方の良さを活用
4. **リアルタイムコラボ**: 外部ツール不要の統合機能

### 参考リンク

- [Zed公式ドキュメント](https://zed.dev/docs/)
- [GitHub: Zed Issues](https://github.com/zed-industries/zed/issues)
- [すべてのコマンド一覧](https://zed.dev/docs/all-actions)

---

## よくある質問（FAQ）

### Q: Zedはまだベータ版ですが、本番環境で使えますか？

2026年春に1.0リリース予定です。現在はベータ版（v0.2xx）ですが:

- **使える**: Rust/Web開発、個人プロジェクト
- **注意が必要**: CPU消費スパイク、エディタのフリーズ、LSP機能の予期しない停止の報告あり
- **待った方が良い**: 本番環境レベルの安定性が必須の場合

### Q: VSCodeから移行すべきですか？

パフォーマンス優先なら移行の価値あり。ただし:

- **拡張機能が少ない**: VSCodeの60,000+に対してZedは数百
- **特殊ツールに依存**: 移行できない可能性が高い（移行者6名全員が拡張機能不足で戻った報告あり）

### Q: M1 MacBook Airでも快適に動きますか？

むしろ低スペック環境ほど効果を実感できます:

- **メモリ**: VSCode 730MB → Zed 142MB（80.5%削減）
- **消費電力**: 61.3%削減
- **起動時間**: 1.2秒 → 0.12秒（10倍高速）

16GB M1 Airなら余裕で動きます。

### Q: GitHub CopilotとClaude Codeどちらを使うべき？

用途で使い分け:

- **GitHub Copilot**: 汎用コード補完、チーム標準
- **Claude Code**: コードレビュー、リファクタリング、複雑な処理の実装

両方同時に使えます。`agent.default_model`で優先するモデルを選択。

### Q: リモート開発はできますか？

できます（2026年1月にWindows対応完了）:

- **サポート**: macOS、Linux、Windows（リモートサーバー）
- **MCPサーバー**: リモートサーバー上でも実行可能

---

## Zedが遅い場合の診断フロー

**ステップ1: 起動時間をチェック**

Zedの起動時間を確認:

- **0.5秒以下** → 正常、ステップ2へ
- **0.5秒以上** → 拡張機能を確認
  - コマンドパレット → `zed: extensions`
  - 不要な拡張機能を無効化

**ステップ2: Agent Panelのレスポンス**

AI補完の速度を確認:

- **遅い** → モデルを変更
  ```json
  {
    "agent": {
      "default_model": {
        "provider": "copilot_chat",
        "model": "gpt-4o"
      }
    }
  }
  ```
- **問題なし** → ステップ3へ

**ステップ3: LSP動作確認**

Language Serverが動作しているか確認:

- コマンドパレット → `debug: open language server logs`
- エラーがあれば、言語サーバーを再インストール
  ```bash
  # Rust
  rustup component add rust-analyzer

  # TypeScript
  npm install -g typescript typescript-language-server
  ```

**ステップ4: ファイルスキャン除外**

大規模プロジェクトの場合:

- `file_scan_exclusions`に除外パスを追加
  ```json
  {
    "file_scan_exclusions": [
      "**/.git",
      "**/target",
      "**/node_modules",
      "**/build",
      "**/dist"
    ]
  }
  ```

**ステップ5: GPU設定**

レンダリングが遅い場合:

- GPUドライバーを最新に更新
- macOS: ソフトウェアアップデート
- Linux: `sudo apt update && sudo apt upgrade`

---

## 他のエディタも使ってる？併用するならこちらもチェック

**VSCode派の人へ:**
- **[VSCode M1 Air 16GB 最適化](https://zenn.dev/fumi_shiki/articles/vscode-m1-air-performance-2026)** - 3秒のフリーズが消える、型チェック10倍速、Copilot削除で常駐プロセス排除

**Cursor使ってる人へ:**
- **[Cursor AI エディタ最適化](https://zenn.dev/fumi_shiki/articles/cursor-performance-tuning-2026)** - インデックス5分→30秒、AI応答61%高速化、HTTP/2問題の解決法

---

# 📖 AI向け詳細設定マニュアル

:::message
**このセクションはAIエージェント向けの詳細設定マニュアルです。**

人間の読者は、上記の「🤖 AIで爆速セットアップ」セクションを使用して、AIに環境構築を任せることをおすすめします。

以下は、AIエージェントが環境構築時に参照する技術仕様とトラブルシューティング情報です。
:::

---

:::details AIアシスタント向けリファレンス（クリックで展開）

## AI Reference: Zed + Claude Code Setup (M1 Air 16GB)

### Core Configuration

```yaml
# パフォーマンスメトリクス
performance_metrics:
  startup_time: 0.12s  # VSCode: 1.2s (10x faster)
  large_project_startup: 0.25s  # VSCode: 3.8s (15.2x faster)
  memory_usage: 142MB  # VSCode: 730MB (80.5% reduction)
  power_consumption: 38.7%  # VSCode: 100% baseline (61.3% reduction)
  input_latency: <10ms  # VSCode: 15-25ms (2.5x faster)
  rendering_fps: 120  # VSCode: 60 (2x smoother)
  file_search_first_match: 32ms  # ripgrep-level speed
  ecosystem_status: Beta (v0.2xx) → 1.0 in Spring 2026

# アーキテクチャ
architecture:
  rendering: GPU direct (custom GPUI framework)
  language: Rust (zero-cost abstractions)
  async: non-blocking LSP requests
  search: SIMD optimizations
  git: Native jj (Jujutsu) integration via version_control_system
  ai_provider: GitHub Copilot + Claude Code Agent
  collaboration: Native multiplayer (channels, calls, screen sharing)

# インストール手順
installation:
  method: brew install --cask zed
  update: brew upgrade --cask zed
  config_path: ~/.config/zed/settings.json

# 必須設定
essential_settings:
  vim_mode: true
  base_keymap: VSCode
  autosave: on_focus_change
  format_on_save: on
  github_copilot_provider: copilot
  github_copilot_inline_completion: subtle  # or eager
  agent_ui_font_size: 13pt  # MUST set explicitly (defaults to 16pt)
  buffer_font_size: 13pt  # Default: 15pt
  ui_font_size: 14pt  # Default: 16pt
  terminal_font_size: 13pt
  buffer_font_family: .ZedMono
  fallbacks: [HackGen Console NF, SF Mono, Menlo]
  file_scan_exclusions: ["**/.git", "**/target", "**/node_modules", "**/build", "**/dist"]
```

### Migration Considerations

```yaml
pros:
  - 10x faster startup
  - 80% less memory
  - 60% less power consumption
  - Native Git/AI/Collaboration
  - 120 FPS GPU rendering

cons:
  - Limited extensions (hundreds vs 60000+)
  - Beta stability issues (CPU spikes, freezes, LSP crashes)
  - Missing: Jupyter notebooks (coming in 1.0), Docker integration

migration_blockers:
  - Special tool dependencies (6 users all returned due to extension gaps)
  - Production-level stability requirements

ideal_for:
  - Performance-critical workflows
  - Resource-constrained hardware (M1 Air)
  - Rust/Web development
  - Minimalist developers
  - Native collaboration needs

stick_with_vscode_if:
  - Require specific extensions
  - Production stability is critical
  - Need Jupyter/Docker integration
  - Team standardization required
```

### Common Issues

```yaml
# トラブルシューティング
troubleshooting:
  agent_panel_font_too_large:
    cause: agent_ui_font_size defaults to ui_font_size (16pt)
    fix: Explicitly set agent_ui_font_size to 13pt

  github_copilot_not_working:
    steps:
      - Restart Zed (Cmd+Q)
      - Verify features.edit_prediction_provider: copilot
      - Check agent.default_model.provider: copilot_chat

  lsp_not_working:
    debug: Command Palette → "debug: open language server logs"
    verify_install: which rust-analyzer / which typescript-language-server
    fix: Reinstall language server

  slow_startup:
    check: startup_time > 0.5s
    action: Disable unnecessary extensions (zed: extensions)

  slow_rendering:
    action: Update GPU drivers (macOS: Software Update, Linux: apt upgrade)
```

### Key Shortcuts (macOS)

```yaml
shortcuts:
  command_palette: Cmd+Shift+P
  file_finder: Cmd+P
  symbol_search: Cmd+T
  agent_panel: Cmd+Shift+A
  recent_threads: Cmd+Shift+J
  review_changes: Shift+Ctrl+R
  git_stage_hunk: Cmd+Y
  git_stage_all: Cmd+Ctrl+Y
  git_commit: Cmd+Enter
  task_runner: Cmd+Shift+R
  terminal: Ctrl+`
```

:::

---

## 拡張機能エコシステム

### 拡張機能の仕組み

- **WebAssembly実行**: 拡張機能はRustで記述され、WebAssemblyにコンパイル
- **サンドボックス実行**: 独立したWebAssemblyランタイム、専用スレッドで実行
- **パフォーマンス維持**: 拡張機能がエディタのパフォーマンスに影響しない設計

### 提供される拡張機能

| カテゴリ | 例 |
|:--------|:---|
| **言語サポート** | Swift, Zig, Kotlin, Prisma, Astro, Haskell, R, Go, Ruby, Elixir |
| **テーマ** | Nord, Material Dark, Darcula, Catppuccin, Gruvbox, Tokyo Night |
| **ユーティリティ** | スペルチェック、フォーマッター、アイコンパック |

### 人気の拡張機能（2026年）

- **Python Snippets**: 生産性向上のためのPythonテンプレート
- **React Snippets**: React/React Native/Redux + TypeScript
- **FastAPI Snippets**: FastAPIのプロダクション対応テンプレート
- **Spell Checker**: マルチ言語対応スペルチェック

### インストール

1. **コマンドパレット** → `zed: extensions`
2. **拡張機能を検索**してインストール
3. または、[公式拡張機能ページ](https://zed.dev/extensions)から閲覧

---

## タスクシステム

### タスクの種類

| タイプ | 場所 | スコープ |
|:------|:-----|:--------|
| **グローバルタスク** | `~/.config/zed/tasks.json` | 全プロジェクト共通 |
| **プロジェクトタスク** | `<project>/.zed/tasks.json` | プロジェクト固有 |

### タスク定義の例

```json
[
  {
    "label": "cargo build",
    "command": "cargo",
    "args": ["build", "--release"],
    "tags": ["rust", "build"]
  },
  {
    "label": "Zenn Preview",
    "command": "npx",
    "args": ["zenn", "preview"],
    "cwd": "./setting",
    "tags": ["zenn"]
  },
  {
    "label": "Run Tests",
    "command": "cargo",
    "args": ["test"],
    "env": {
      "RUST_BACKTRACE": "1"
    }
  }
]
```

### 環境変数の利用

| 変数 | 説明 |
|:----|:----|
| `$ZED_FILE` | 現在のファイルパス |
| `$ZED_COLUMN` | カーソルの列番号 |
| `$ZED_ROW` | カーソルの行番号 |
| `$ZED_DIRNAME` | 現在のファイルのディレクトリ |
| `$ZED_WORKTREE_ROOT` | プロジェクトルート |
| `$ZED_SYMBOL` | 現在のシンボル |
| `$ZED_SELECTED_TEXT` | 選択テキスト |
| `$ZED_FILENAME` | ファイル名 |
| `$ZED_STEM` | 拡張子なしファイル名 |

---

## 統合ターミナル

### ターミナルの特徴

- **バックエンド**: Alacrittyターミナルエミュレータを使用
- **統合**: エディタ内で完結、タブとして扱える
- **タスク実行**: タスクシステムと連携

### ターミナルを開く

- **ショートカット**: `Ctrl+\`` (バッククォート)
- **タブバー**: 右側の `+` アイコンをクリック

### ターミナル設定

```json
{
  "terminal": {
    "font_size": 13.0,
    "font_family": "HackGen Console NF",
    "line_height": "comfortable",
    "blinking": "terminal_controlled",
    "alternate_scroll": "on",
    "option_as_meta": false,
    "copy_on_select": false,
    "button": true,
    "shell": {
      "program": "/bin/zsh",
      "args": ["-l"]
    },
    "env": {
      "TERM": "xterm-256color"
    }
  }
}
```

---

## デバッグ機能

### Debug Adapter Protocol (DAP) 対応

Zedは2025年6月に統合デバッガーをリリース。**DAP (Debug Adapter Protocol)** を採用。

#### サポート言語

| 言語 | デバッグアダプター | インライン値表示 |
|:----|:----------------|:---------------|
| **Rust** | lldb / CodeLLDB | ✅ |
| **C/C++** | lldb / gdb | ✅ |
| **Python** | debugpy | ✅ |
| **JavaScript/TypeScript** | Node Debug | ❌ |
| **Go** | Delve | ✅ |

#### デバッグの開始

1. **ブレークポイント設定**: 行番号をクリック
2. **デバッグ設定**: プロジェクト内に `.zed/launch.json` を作成（自動生成対応）
3. **デバッグ開始**: コマンドパレット → `debugger: start`

#### launch.json の例（Rust）

```json
{
  "version": "0.1.0",
  "configurations": [
    {
      "type": "lldb",
      "request": "launch",
      "name": "Debug Rust",
      "program": "${workspaceFolder}/target/debug/myapp",
      "args": [],
      "cwd": "${workspaceFolder}"
    }
  ]
}
```

---

## スニペット/テンプレート

### スニペットの場所

- **ディレクトリ**: `~/.config/zed/snippets/`
- **開き方**: コマンドパレット → `snippets: configure snippets`

### スニペット定義の例

```json
{
  "Rust Test Function": {
    "prefix": "test",
    "body": [
      "#[test]",
      "fn ${1:test_name}() {",
      "    ${0:// test body}",
      "}"
    ],
    "description": "Create a Rust test function"
  },
  "Println": {
    "prefix": "pln",
    "body": "println!(\"${1}\");$0",
    "description": "Print to stdout"
  }
}
```

### プレースホルダー構文

| 構文 | 説明 |
|:----|:----|
| `$1`, `$2` | タブストップ（Tabキーで移動） |
| `${1:default}` | デフォルト値付きプレースホルダー |
| `$0` | 最終カーソル位置 |
| `${1:text}` と `$1` | 同じ番号は連動（同時編集） |

---

## プロジェクト設定

`.zed/settings.json`でプロジェクト固有の設定が可能：

```json
{
  "languages": {
    "Markdown": {
      "soft_wrap": "editor_width",
      "tab_size": 2,
      "formatter": {
        "external": {
          "command": "npx",
          "arguments": ["prettier", "--parser", "markdown"]
        }
      }
    }
  },
  "file_scan_exclusions": ["**/docs"]
}
```

---

## カスタムキーバインド

`~/.config/zed/keymap.json`で独自のショートカットを設定：

```json
[
  {
    "bindings": {
      "cmd-left": "workspace::ActivatePaneLeft",
      "cmd-right": "workspace::ActivatePaneRight",
      "ctrl-right": "editor::SelectLargerSyntaxNode",
      "ctrl-left": "editor::SelectSmallerSyntaxNode"
    }
  },
  {
    "context": "VimControl",
    "bindings": {
      "ctrl-w h": "workspace::ActivatePaneLeft",
      "ctrl-w l": "workspace::ActivatePaneRight"
    }
  }
]
```

キーマップエディタ: `Cmd+K Cmd+S`

---

## AI機能（2026年）

### MCP（Model Context Protocol）

メモリサーバー接続でコンテキストを永続化：

```json
{
  "context_servers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    }
  }
}
```

### External Agents

ACP（Agent Client Protocol）経由でサードパーティエージェント統合可能。

### Claude Code統合

- `@`メンションでファイル、スレッド、シンボル、Webフェッチ
- マルチモーダル対応（画像、PDF）
- コードレビュー機能（`Shift+Ctrl+R`）

---

## コラボレーション機能

| 機能 | 説明 |
|:----|:----|
| プロジェクト共有 | Shareボタンからチャンネル経由で共有 |
| マルチユーザー編集 | CRDT、プレゼンス表示、共有カーソル |
| Follow User | 他ユーザーのカーソルをフォロー |
| Shared Terminal | ターミナルセッション共有 |
| 音声・画面共有 | 組み込み機能（外部ツール不要） |

**セットアップ**: GitHubアカウントのみ（α版、無料）

---

## リモート開発

### アーキテクチャ

- **ローカルマシン**: ZedのUI、LLM、Tree-sitter
- **リモートサーバー**: ソースコード、LSP、タスク、ターミナル

### サポートプラットフォーム（2026年1月更新）

| プラットフォーム | ローカル | リモート |
|:---------------|:--------|:--------|
| macOS | ✅ | ✅ |
| Linux | ✅ | ✅ |
| Windows | ✅ | ✅（2026年1月対応） |

### 初回セットアップ

1. **SSH設定**: `~/.ssh/config` にリモートホストを定義
2. **接続**: コマンドパレット → `remote: connect to server`
3. **プロジェクトを開く**: リモートサーバー上のディレクトリを選択

### リモート設定の例

```json
{
  "ssh_connections": [
    {
      "host": "dev-server",
      "projects": ["/home/user/projects"]
    }
  ]
}
```

### MCPサーバーのリモート実行（2026年1月新機能）

リモート開発時に、MCPサーバーをリモートサーバー上で実行可能：

```json
{
  "context_servers": {
    "my-mcp-server": {
      "command": "node",
      "args": ["server.js"],
      "remote": true
    }
  }
}
```

---

## パフォーマンスチューニング

### 2026年の主な改善点

| 改善項目 | 内容 |
|:--------|:----|
| **バイナリファイル処理** | バイナリファイルを開こうとした際のメモリ使用量削減 |
| **Agent Panel** | 大規模diff表示時のレンダリング高速化 |
| **マルチバッファー** | 多数行表示時のディスプレイマップレンダリング改善 |

### パフォーマンス設定

```json
{
  "file_scan_exclusions": [
    "**/.git",
    "**/target",
    "**/node_modules",
    "**/.jj",
    "**/.DS_Store",
    "**/build",
    "**/dist"
  ],
  "hard_tabs": false,
  "tab_size": 4,
  "show_whitespaces": "none",
  "gutter": {
    "line_numbers": true,
    "code_actions": false
  }
}
```

### ベストプラクティス

1. **大規模ディレクトリの除外**: `file_scan_exclusions` でビルド成果物を除外
2. **不要な機能を無効化**: `code_actions` など、頻繁に使わない機能を無効化
3. **拡張機能の最小化**: 必要な拡張機能のみインストール
4. **GPU設定**: GPUドライバーを最新に保つ

---

## Claude Code活用術

### 効果的なプロンプト例

**コードレビュー依頼**:
```
選択したコードをレビューして、以下の観点で指摘してください：
- パフォーマンスの問題
- セキュリティリスク
- 可読性の改善点
```

**リファクタリング**:
```
この関数を以下の方針でリファクタリングしてください：
- 関数を小さく分割
- エラーハンドリングを追加
- ドキュメントコメントを追加
```

**テスト生成**:
```
この関数のユニットテストをJestで生成してください。
エッジケースとエラーケースも含めてください。
```

### @メンション活用

- `@file src/main.rs`: 特定ファイルをコンテキストに追加
- `@symbol UserService`: 特定のクラス・関数を参照
- `@thread`: 過去のスレッドを参照
- `@web https://example.com`: Webページをフェッチして参照

### ワークフロー例

1. **バグ修正フロー**:
   - `Cmd+Shift+A`でAgent Panel起動
   - 問題のコードを選択→`agent::AddSelectionToThread`
   - 「このコードのバグを特定して修正してください」

2. **機能追加フロー**:
   - `@file`で関連ファイルを追加
   - 「○○機能を追加してください。既存のパターンに従ってください」
   - `Shift+Ctrl+R`で変更を一括レビュー

3. **コードレビューフロー**:
   - Git Panel（`Cmd+Y`）で変更を確認
   - Agent Panelで「この変更をレビューしてください」
   - 指摘に従って修正→再レビュー

---

*最終更新: 2026-02-04*
