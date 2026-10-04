# Google Cloud AI ハンズオン

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Google Cloud の AI 機能を、実際のデータに当てて試すハンズオンです。  
UCI Online Retail Dataset（英国の雑貨卸の取引データ）を題材にしています。

## 構成

| #  | テーマ                                       | 主な技術                                | 状態   |
|----|----------------------------------------------|-----------------------------------------|--------|
| 00 | データの準備（xlsx → BigQuery）              | pandas, BigQuery                        | 準備中 |
| 01 | BigQuery の AI 関数で、商品にカテゴリを付ける | AI.GENERATE, AI.CLASSIFY, AI.EMBED      | 準備中 |
| 02 | Agent Platform で分析エージェントを作る      | Gemini Enterprise Agent Platform        | 予定   |

01 と 02 は、どちらも 00 で作るテーブルを使います。02 は 01 で付けたカテゴリも使います。

## データセット

**UCI Online Retail Dataset**  
出典: Chen, D. (2015). [Online Retail](https://doi.org/10.24432/C5BW33). UCI Machine Learning Repository. CC BY 4.0

- 使う期間: 2010-12-01 〜 2011-02-28（3か月）
- データ本体はリポジトリに含めていません。ダウンロード手順は [data/README.md](data/README.md) を見てください

## 準備

```bash
uv sync
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
```

## ディレクトリ構成

```text
.
├── 00_setup/          # データの準備（各回で共通）
├── 01_ai_tagging/     # BigQuery の AI 関数で商品にカテゴリを付ける
├── 02_analysis_agent/ # Agent Platform で分析エージェントを作る
└── data/              # ローカルのデータ置き場（.gitignore で除外）
```
