name: Kalshi Crypto Bot

on:
  schedule:
    - cron: '*/5 13-20 * * 1-5'
  workflow_dispatch:

env:
  KALSHI_API_KEY: ${{ secrets.KALSHI_API_KEY }}
  KALSHI_API_SECRET: ${{ secrets.KALSHI_API_SECRET }}

jobs:
  trade:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          cache: 'pip'
      - run: pip install requests
      - run: python bot.py
      - uses: actions/upload-artifact@v4
        with:
          name: memory-bank
          path: bot_memory.db
          retention-days: 30
