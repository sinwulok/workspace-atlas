# binance-multi-assets-singal-agent

Multi-asset Binance trading signal agent prototype with backend and frontend structure.

---

## Overview

A multi-asset crypto trading bot that uses technical indicators such as MACD to automate trading on Binance. This bot fetches historical data, applies trading logic, and simulates or executes trades on the Binance Testnet.

---

## Category / Lifecycle / Tags

- **Category**: Development
- **Type**: Quant | Signal | Feature Extraction
- **Lifecycle**: stable
- **Tags**: trading, quant, binance, agent

---

## Project Structure
  ```
binance-trading-base/
├── backend/                  # Python FastAPI 專案
│   ├── app/
│   │   ├── __init__.py
│   │   ├── api/              # API 端點 (Routes)
│   │   │   ├── __init__.py
│   │   │   ├── endpoints/
│   │   │   │   ├── __init__.py
│   │   │   │   └── bot_control.py  # 控制機器人啟動/停止/狀態的 API
│   │   │   └── websocket.py      # WebSocket 即時通訊端點
│   │   ├── core/
│   │   │   ├── __init__.py
│   │   │   └── config.py         # 讀取 API 金鑰和設定
│   │   ├── services/
│   │   │   ├── __init__.py
│   │   │   ├── binance_service.py # 封裝與幣安 API 的所有互動 (OOP)
│   │   │   ├── indicator_service.py # 封裝所有技術指標計算 (MACD 等)
│   │   │   └── trading_bot.py     # 核心交易機器人邏輯 (OOP Class)
│   │   └── main.py               # FastAPI 應用程式進入點
│   ├── .env                    # 儲存 API 金鑰 (重要！不要上傳到 Git)
│   └── requirements.txt
│
├── frontend/                 # React 專案
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── api/
│   │   │   └── botApi.js         # 呼叫後端 API 的函式
│   │   ├── components/
│   │   │   ├── BotController.js  # 包含開始/停止按鈕的組件
│   │   │   ├── Dashboard.js      # 主儀表板
│   │   │   ├── LogStream.js      # 顯示即時日誌的組件
│   │   │   └── AssetStatus.js    # 顯示各個資產狀態的組件
│   │   ├── hooks/
│   │   │   └── useWebSocket.js   # 自訂 hook 用於處理 WebSocket 連線
│   │   ├── App.js
│   │   └── index.js
│   ├── package.json
│
└── README.md
  ```

---

## Demo

![MACD 指標圖](pubclic/assets/macd-of-closing.png)

![BTCUSDT Closing Price with Signals](pubclic/assets/BTCUSDT-closing-price-with-signals.png)

---

## Features

- Fetches historical 1-minute bars from Binance
- Calculates MACD and percentage price change indicators
- Determines buy/sell signals based on the trading strategy
- Supports multiple assets
- Interactive setup for API keys and asset configurations
- Option to import asset data from .csv or .txt files

---

## Setup
1. Clone the repository:
  ```sh
  git clone https://github.com/yourusername/binance-assets-agent-macd.git
  cd binance-assets-agent-macd
  ```

---

## Installation
2. Install the required packages:
  ```sh
  pip install -r requirements.txt
  ```

3. Configure your Binance API keys in a `.env` file:
  ```
  BINANCE_API_KEY=your_api_key
  BINANCE_API_SECRET=your_api_secret
  ```

---

## Usage
### Running the Bot
1. Ensure you have your Binance API key and secret ready.
2. Run the bot:
  ```sh
  python -m main_agent
  ```
3. Follow the prompts to enter your API information and configure your assets.

---

### Importing Assets from a File
1. Place your assets.csv or assets.txt file in the data/ directory.
2. The file should have the following structure:
  ```
  asset,is_long,order_size
  BTC,False,[size]
  LTC,False,100
  TRX,False,1000
  ETH,False,0.0003
  BNB,False,0.0025
  XRP,False,100
  ```
3. Run the bot and choose the option to import assets from the file.

---

## License
This project is licensed under the MIT License.

---

## Acknowledgements

### Binance API
A big thanks to the [Binance API](https://github.com/sammchardy/python-binance) project which provides a comprehensive Python API for the Binance trading platform. 

Here's a quick example of how to use the Binance API to fetch account information:
  ```python
  from binance.client import Client
  
  api_key = 'your_api_key'
  api_secret = 'your_api_secret'
  client = Client(api_key, api_secret, testnet=True)
  
  # Get account information
  account_info = client.get_account()
  print(account_info)
  ```

---

## Contact

For any questions or suggestions, please open an issue or contact me at this project!

Thank you for using the Binance Trading Bot! Happy trading! 📈

---

## Related Links

- [Project Catalog](../../catalog/index.md)
- [Repository Root](../../README.md)
