# 密码管理器 / Password Manager / パスワードマネージャー

[中文](#中文) | [English](#english) | [日本語](#日本語)

---

## 中文

一个单文件、零依赖的本地密码管理器。所有数据加密存储在浏览器本地，不联网，不上传。

**在线使用：** https://shinnaaa.github.io/Password-Manager/

### 功能

- **密码生成器** — 可调长度、字符集，实时显示强度与熵值
- **密码库** — 增删改查，搜索，标签分类，显示/隐藏，一键复制（30 秒自动清除剪贴板）
- **Secret 管理** — 存储 API Key、Token、SSH Key、Connection String 等，支持环境标记（开发/测试/生产）和过期提醒
- **TOTP 动态码** — 内置 Google Authenticator 兼容的 6 位验证码生成
- **健康报告** — 检测重复密码、弱密码、长期未更新、以及即将过期/已过期的 Secret
- **加密导出 / 导入** — 备份文件使用主密码加密，可存入网盘实现多设备同步
- **自动锁定** — 5 分钟无操作自动锁定

### 安全

| 机制 | 实现 |
|------|------|
| 加密算法 | AES-256-GCM |
| 密钥派生 | PBKDF2（210,000 次迭代，SHA-256） |
| 随机数 | `crypto.getRandomValues()`（无模偏差） |
| 存储位置 | 浏览器 `localStorage`（仅存加密密文） |
| 网络请求 | 无 |

### 本地使用

直接用浏览器打开 `index.html` 即可，无需安装任何依赖。

---

## English

A single-file, zero-dependency local password manager. All data is encrypted and stored in your browser locally — no network requests, no uploads.

**Live demo:** https://shinnaaa.github.io/Password-Manager/

### Features

- **Password Generator** — Configurable length and character sets with real-time strength and entropy display
- **Password Vault** — Full CRUD, search, tag filtering, show/hide, one-click copy (clipboard auto-cleared after 30 seconds)
- **Secret Management** — Store API Keys, Tokens, SSH Keys, Connection Strings, etc. with environment tags (dev/staging/prod) and expiry reminders
- **Built-in TOTP** — Google Authenticator-compatible 6-digit code generation
- **Health Report** — Detects duplicate passwords, weak passwords, stale entries, and expired/expiring Secrets
- **Encrypted Export / Import** — Backup files are encrypted with your master password; store in cloud drives for multi-device sync
- **Auto-lock** — Automatically locks after 5 minutes of inactivity

### Security

| Mechanism | Implementation |
|-----------|---------------|
| Encryption | AES-256-GCM |
| Key derivation | PBKDF2 (210,000 iterations, SHA-256) |
| Randomness | `crypto.getRandomValues()` (no modulo bias) |
| Storage | Browser `localStorage` (encrypted ciphertext only) |
| Network requests | None |

### Local Usage

Open `index.html` directly in any modern browser. No installation or dependencies required.

---

## 日本語

シングルファイル・ゼロ依存のローカルパスワードマネージャーです。すべてのデータはブラウザ内で暗号化して保存され、ネットワーク通信は一切行いません。

**オンラインで使う：** https://shinnaaa.github.io/Password-Manager/

### 機能

- **パスワードジェネレーター** — 文字数・文字種を自由に設定、強度とエントロピーをリアルタイム表示
- **パスワード保管庫** — 追加・編集・削除・検索、タグ分類、表示/非表示、ワンクリックコピー（30 秒後にクリップボードを自動消去）
- **Secret 管理** — API Key・Token・SSH Key・接続文字列などを保存。環境タグ（開発/テスト/本番）や有効期限アラートに対応
- **内蔵 TOTP** — Google Authenticator 互換の 6 桁ワンタイムコードを生成
- **健全性レポート** — パスワードの使い回し・脆弱なパスワード・長期未更新・期限切れ/期限間近の Secret を検出
- **暗号化エクスポート / インポート** — バックアップファイルはマスターパスワードで暗号化。クラウドストレージ経由で複数デバイス間同期が可能
- **自動ロック** — 5 分間操作がない場合に自動ロック

### セキュリティ

| 仕組み | 実装内容 |
|--------|---------|
| 暗号化アルゴリズム | AES-256-GCM |
| 鍵導出 | PBKDF2（210,000 回反復、SHA-256） |
| 乱数生成 | `crypto.getRandomValues()`（モジュロバイアスなし） |
| 保存場所 | ブラウザの `localStorage`（暗号化済み密文のみ） |
| 通信 | なし |

### ローカルで使う

`index.html` をブラウザで直接開くだけで使えます。インストール不要・依存関係なし。
