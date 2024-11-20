# Wbt
Cripto
from binance.client import Client
import time

# Введіть свої API ключі тут
api_key = 'your_api_key'
api_secret = 'your_api_secret'

# Ініціалізація клієнта
client = Client(api_key, api_secret)

# Функція для перевірки балансу
def get_balance():
    balance = client.get_account()
    for asset in balance['balances']:
        if float(asset['free']) > 0:
            print(f"Asset: {asset['asset']}, Balance: {asset['free']}")

# Функція для купівлі криптовалюти
def buy_crypto(symbol, amount):
    order = client.order_market_buy(
        symbol=symbol,
        quantity=amount
    )
    print(order)

# Функція для продажу криптовалюти
def sell_crypto(symbol, amount):
    order = client.order_market_sell(
        symbol=symbol,
        quantity=amount
    )
    print(order)

# Основна логіка бота
def trade():
    symbol = 'BTCUSDT'  # Пара криптовалют (наприклад, BTC/USDT)
    buy_amount = 0.001  # Кількість криптовалюти для покупки
    sell_amount = 0.001  # Кількість криптовалюти для продажу

    # Логіка: купувати, коли ціна падає, і продавати, коли ціна росте
    while True:
        # Отримуємо поточну ціну
        ticker = client.get_symbol_ticker(symbol=symbol)
        price = float(ticker['price'])
        
        # Проста стратегія: купувати, коли ціна менша за 20000, продавати, коли більше за 25000
        if price < 20000:
            print(f"Buy {symbol} at {price}")
            buy_crypto(symbol, buy_amount)
        elif price > 25000:
            print(f"Sell {symbol} at {price}")
            sell_crypto(symbol, sell_amount)

        time.sleep(60)  # Затримка між перевірками (1 хвилина)

if __name__ == '__main__':
    trade()
    
