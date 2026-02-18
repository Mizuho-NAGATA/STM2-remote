# INFICON STM‑2 Remote — Real‑time STM‑2 .log Monitoring (InfluxDB + Grafana) (UNOFFICIAL)

[![Python Lint and Check](https://github.com/Mizuho-NAGATA/STM2-remote/actions/workflows/python-lint.yml/badge.svg)](https://github.com/Mizuho-NAGATA/STM2-remote/actions/workflows/python-lint.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

---

## 📖 English | [日本語](#日本語版)

### Overview

System for remote monitoring of .log files from the **INFICON STM-2 USB Thin Film Deposition Rate/Film Thickness Monitor**. Visualizes data in real time over the network using **InfluxDB** and **Grafana**. This repository includes a ready-to-use Grafana dashboard (JSON).

![外部向け説明資料](https://github.com/user-attachments/assets/eb5fce0c-8dbf-4847-b3d2-5c2d21164ab5)

### ✨ Features

- 📊 Real-time monitoring of STM-2 film thickness, deposition rate, and frequency
- 🌐 Simultaneous multi-site monitoring via network
- 🚨 Panel lights up red to notify when thickness exceeds 80% of target thickness
- 🎯 Support for multiple deposition materials with automatic density/Z-ratio configuration
- 📁 Simple drag-and-drop log file selection

![Alert notification](https://github.com/user-attachments/assets/13df291b-82ce-4b08-9643-8e03dbeeca35)

### ⚠️ Disclaimer

- This program is **NOT** an official INFICON product
- The author does not provide commercial support
- Network configuration and security measures should be implemented according to your organization's policies
- The accuracy of physical property values used in this system is not guaranteed
- The author is not responsible for any consequences resulting from the use of this software
- Designed for STM-2 attached to electron beam deposition systems

---

## 日本語版

### 概要

INFICON STM-2 USB 薄膜蒸着レート/膜厚モニター の.logファイルを遠隔監視するためのシステム。**InfluxDB** と **Grafana** を用いてネットワーク越しにリアルタイムで可視化します。このリポジトリには、すぐに利用できる Grafana ダッシュボード（JSON）が含まれています。

### ✨ 特長

- 📊 STM-2 の膜厚・成膜レート・周波数をリアルタイム監視
- 🌐 ネットワーク経由での多地点同時監視
- 🚨 目標厚さの80%を超えるとパネルが赤く点灯してお知らせします
- 🎯 複数の蒸着材料をサポート、密度・Z-ratioを自動設定
- 📁 ログファイルのドラッグ&ドロップ選択に対応

### ⚠️ 注意事項

- このプログラムはINFICON社の**公式なものではありません**
- 本リポジトリの著者は商用サポートを提供するものではありません
- ネットワーク構成やセキュリティ対策は各組織のポリシーに従って実施してください
- 本システムで使用する物性値について、正確性を保証するものではありません
- 利用により生じたいかなる結果についても、作者は責任を負いません
- 電子ビーム蒸着装置に取り付けられたSTM-2を想定して作成

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- InfluxDB v1.x (recommended for compatibility)
- Grafana

### Installation

```bash
# Clone the repository
git clone https://github.com/Mizuho-NAGATA/STM2-remote.git
cd STM2-remote

# Install dependencies
pip install -r requirements.txt
```

---

## STM-2接続パソコンの準備：

### 🪟 Windows の場合
Windows Defender ファイアウォールに受信規則を追加してポート3000を開放する。  
固定IPアドレスを設定する。あらかじめネットワーク管理者に確認することをおすすめします。 

#### Pythonをインストール  
公式サイト： <a href="https://www.python.org/" target="blank">https://www.python.org/</a>  

コマンドプロンプトで下記のコマンドを実行して必要なライブラリをインストールする。  
```cmd
pip install influxdb customtkinter tkinterdnd2
```

または requirements.txt を使用：
```cmd
pip install -r requirements.txt
```

#### InfluxDBをインストール  
公式サイト： <a href="https://www.influxdata.com/" target="blank">https://www.influxdata.com/</a>     
STM-2 のログスクリプトとの互換性のため、InfluxDB v1.x を推奨します。  

#### Grafanaをインストール  
公式サイト： <a href="https://grafana.com/" target="_blank"> https://grafana.com/ </a>

"STM-2_dashboard.json" をインポートして各種設定を完了させる。  
- Grafana → Dashboards → Import  
- JSON Upload または JSON を貼り付け  
- Data source を InfluxDB に設定  

---

### 🍎 macOS の場合
ファイアウォール設定でポート3000を開放する。  
固定IPアドレスを設定する。あらかじめネットワーク管理者に確認することをおすすめします。

#### Pythonをインストール  
公式サイト： <a href="https://www.python.org/" target="blank">https://www.python.org/</a>  
または Homebrew を使用：
```bash
brew install python3
```

ターミナルで下記のコマンドを実行して必要なライブラリをインストールする。  
```bash
pip3 install influxdb customtkinter tkinterdnd2
```

または requirements.txt を使用：
```bash
pip3 install -r requirements.txt
```

#### InfluxDBをインストール  
Homebrew を使用してインストール：
```bash
brew install influxdb@1
brew services start influxdb@1
```

または公式サイト： <a href="https://www.influxdata.com/" target="blank">https://www.influxdata.com/</a>  

#### Grafanaをインストール  
Homebrew を使用してインストール：
```bash
brew install grafana
brew services start grafana
```

または公式サイト： <a href="https://grafana.com/" target="_blank"> https://grafana.com/ </a>

"STM-2_dashboard.json" をインポートして各種設定を完了させる。  
- Grafana → Dashboards → Import  
- JSON Upload または JSON を貼り付け  
- Data source を InfluxDB に設定  

---

### 🐧 Linux の場合
ファイアウォール設定（iptables または firewalld）でポート3000を開放する。  
固定IPアドレスを設定する。あらかじめネットワーク管理者に確認することをおすすめします。

#### Pythonをインストール  
多くの Linux ディストリビューションには Python3 がプリインストールされています。  
未インストールの場合：
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip

# Fedora/RHEL/CentOS
sudo dnf install python3 python3-pip
```

ターミナルで下記のコマンドを実行して必要なライブラリをインストールする。  
```bash
pip3 install influxdb customtkinter tkinterdnd2
```

または requirements.txt を使用：
```bash
pip3 install -r requirements.txt
```

**注意**: 日本語フォントが必要です。未インストールの場合：
```bash
# Ubuntu/Debian
sudo apt install fonts-noto-cjk

# Fedora/RHEL/CentOS
sudo dnf install google-noto-sans-cjk-jp-fonts
```

#### InfluxDBをインストール  
公式サイトの手順に従ってインストール： <a href="https://www.influxdata.com/" target="blank">https://www.influxdata.com/</a>  

Ubuntu/Debian の場合：
```bash
wget https://dl.influxdata.com/influxdb/releases/influxdb_1.8.10_amd64.deb
sudo dpkg -i influxdb_1.8.10_amd64.deb
sudo systemctl start influxdb
sudo systemctl enable influxdb
```

#### Grafanaをインストール  
公式サイトの手順に従ってインストール： <a href="https://grafana.com/" target="_blank"> https://grafana.com/ </a>

Ubuntu/Debian の場合：
```bash
sudo apt-get install -y software-properties-common
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://packages.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get install grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

"STM-2_dashboard.json" をインポートして各種設定を完了させる。  
- Grafana → Dashboards → Import  
- JSON Upload または JSON を貼り付け  
- Data source を InfluxDB に設定  

---
## 動作手順：
## 🖥️ **STM‑2 接続パソコンで行う作業**

### 1. **STM‑2専用ソフトウェア（INFICON）**
- INFICON公式 STM‑2 ソフトを起動  
- 必要な設定を行い、**記録 Start**

### 2. **InfluxDB の起動**
- InfluxDB のフォルダへ移動  
- Shift＋右クリック → **「ここでコマンドウィンドウを開く」**  
- コマンドプロンプトで  
  ```
  .\influxd
  ```  
  を実行し、InfluxDB を起動

### 3. **Python GUI（蒸着モニタリングアプリ）**
- Python コードを実行して GUI を起動
- 目標厚さ（nm）を入力  
- 蒸着材料を選択 → **密度・Z‑ratio が自動入力**  
- 「参照」ボタンから **STM‑2 のログファイル（現在記録中のもの）** を選択  
- GUI が InfluxDB にデータを書き込み始める
![GUI](https://github.com/user-attachments/assets/0c668087-c73f-4ab3-9ee0-d0cd39099132)


---

## 💻 **クライアントPC（遠隔監視側）で行う作業**

### 1. **Grafana へアクセス**
- Webブラウザを開く  
- STM‑2接続PCの固定IPアドレスを指定してアクセス  
  ```
  http://（STM‑2接続PCの固定IP）:3000
  ```
- Grafana ダッシュボードでリアルタイム監視

---

## 著者  
Copyright (c) 2026 NAGATA Mizuho, 永田 みず穂 - Institute of Laser Engineering, The University of Osaka

---

## 🤝 Contributing / 貢献

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details.

貢献を歓迎します！詳細は [CONTRIBUTING.md](CONTRIBUTING.md) をお読みください。

---

## 🛡️ Security / セキュリティ

For security concerns, please see [SECURITY.md](SECURITY.md).

セキュリティに関する懸念事項は [SECURITY.md](SECURITY.md) をご覧ください。

---

## 🐛 Troubleshooting / トラブルシューティング

### Common Issues / よくある問題

#### InfluxDB Connection Error / InfluxDB 接続エラー

**Problem:** Cannot connect to InfluxDB

**Solution:**
- Ensure InfluxDB is running: `influxd` (Windows) or check service status on Linux/macOS
- Verify the database name matches the configuration (default: "stm2")
- Check firewall settings

**問題:** InfluxDB に接続できません

**解決策:**
- InfluxDB が実行中であることを確認: Windows では `influxd`、Linux/macOS ではサービスステータスを確認
- データベース名が設定と一致しているか確認（デフォルト: "stm2"）
- ファイアウォール設定を確認

#### Log File Not Found / ログファイルが見つからない

**Problem:** "ログファイルが存在しません" error

**Solution:**
- Ensure the STM-2 software is recording data
- Verify the file path is correct
- Check file permissions

**問題:** "ログファイルが存在しません" エラー

**解決策:**
- STM-2 ソフトウェアがデータを記録していることを確認
- ファイルパスが正しいか確認
- ファイルのアクセス権限を確認

#### Japanese Font Not Displaying / 日本語フォントが表示されない

**Problem:** GUI shows square boxes instead of Japanese characters (Linux only)

**Solution:**
```bash
# Ubuntu/Debian
sudo apt install fonts-noto-cjk

# Fedora/RHEL/CentOS
sudo dnf install google-noto-sans-cjk-jp-fonts
```

**問題:** GUI で日本語が四角で表示される（Linux のみ）

**解決策:** 上記のコマンドで日本語フォントをインストール

#### Grafana Dashboard Not Showing Data / Grafana ダッシュボードにデータが表示されない

**Problem:** Dashboard is empty or shows "No Data"

**Solution:**
- Verify the Python monitoring script is running
- Check the data source configuration in Grafana
- Ensure the correct database name is set in Grafana data source
- Check the time range in Grafana (top-right corner)

**問題:** ダッシュボードが空、または「No Data」と表示される

**解決策:**
- Python モニタリングスクリプトが実行中であることを確認
- Grafana のデータソース設定を確認
- Grafana データソースで正しいデータベース名が設定されているか確認
- Grafana の時間範囲を確認（右上隅）

### Getting Help / ヘルプを得る

If you encounter other issues:
1. Check existing [Issues](https://github.com/Mizuho-NAGATA/STM2-remote/issues)
2. Create a new Issue with detailed information about your problem

その他の問題が発生した場合：
1. 既存の [Issues](https://github.com/Mizuho-NAGATA/STM2-remote/issues) を確認
2. 問題の詳細情報を含む新しい Issue を作成

---

## 📋 Supported Materials / サポート材料

The application includes pre-configured settings for the following materials:

アプリケーションには以下の材料の事前設定が含まれています：

| Material | Density (g/cm³) | Z-ratio |
|----------|----------------|---------|
| Al       | 2.699          | 1.08    |
| Au       | 19.320         | 0.381   |
| CaO      | 3.350          | 1.000   |
| Cr       | 7.19           | 0.305   |
| Cu       | 8.96           | 0.437   |
| Fe       | 7.874          | 0.349   |
| Ge       | 5.323          | 0.516   |
| Mg       | 1.740          | 1.610   |
| Mn       | 7.44           | 0.377   |
| Pb       | 11.350         | 1.13    |
| Sn       | 7.310          | 0.72    |
| Tb       | 8.229          | 0.66    |
| Ti       | 4.54           | 0.628   |

Custom materials can be configured by entering values manually in the GUI.

カスタム材料は GUI で手動で値を入力することで設定できます。

---

## 著者  
Copyright (c) 2026 NAGATA Mizuho, 永田 みず穂 - Institute of Laser Engineering, The University of Osaka
---

## ライセンス License
このプロジェクトはMITライセンスの下で公開されています。ライセンスの全文については、[LICENSE](LICENSE) をご覧ください。  

This project is released under the MIT License. For the full text of the license, please see the [LICENSE](LICENSE) file.

---

## 謝辞 Acknowledgments
本開発は文部科学省先端研究基盤共用促進事業（先端研究設備プラットフォームプログラム） JPMXS0450300021である[パワーレーザーDXプラットフォーム](https://powerlaser.jp/)で共用された機器を利用した成果です。

This work was the result of using research equipment shared by the [Power Laser DX Platform](https://powerlaser.jp/), which is MEXT Project for promoting public utilization of advanced research infrastructure (Program for advanced research equipment platforms) Grant Number JPMXS0450300021.

---

## 📚 Documentation / ドキュメント

- [CONTRIBUTING.md](CONTRIBUTING.md) - Contribution guidelines / 貢献ガイドライン
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) - Code of conduct / 行動規範
- [SECURITY.md](SECURITY.md) - Security policy / セキュリティポリシー
- [config.example.yml](config.example.yml) - Example configuration / 設定例

---

## 🔗 Links / リンク

- [INFICON](https://www.inficon.com/) - Official INFICON website
- [InfluxDB](https://www.influxdata.com/) - Time series database
- [Grafana](https://grafana.com/) - Data visualization platform

---

## ⭐ Support / サポート

If you find this project useful, please consider giving it a star ⭐!

このプロジェクトが役に立つと思われた場合は、スターをつけてください ⭐！

