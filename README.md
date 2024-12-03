import ccxt
import time

# إعدادات الاتصال بالمنصة (استبدل 'exchange_name' بمزود خدمة التداول الخاص بك)
exchange = ccxt.binance({'apiKey': 'YOUR_API_KEY', 'secret': 'YOUR_SECRET'})

def check_market(symbol):
    # استعلام عن البيانات الحالية للسوق
    ticker = exchange.fetch_ticker(symbol)
    return ticker['last']

def trade(symbol, amount):
    price = check_market(symbol)
    print(f'Trading at price: {price}')
    
    # هنا يمكنك وضع الاستراتيجية الخاصة بك، مثلاً:
    # 1. إذا كان السعر مرتفعًا بنسبة معينة، ضع شراء.
    # 2. إذا كان السعر منخفضًا بنسبة معينة، ضع بيع.
    
    # مثال على تنفيذ صفقة
    # exchange.create_market_order(symbol, 'buy', amount)  # شراء
    # exchange.create_market_order(symbol, 'sell', amount)  # بيع

def main():
    symbol = 'BTC/USDT'  # استبدل برمز الخيار الخاص بك
    amount = 0.01  # الكمية المراد تداولها
    
    while True:
        try:
            trade(symbol, amount)
            time.sleep(60)  # الانتظار لمدة دقيقة قبل إجراء الصفقة التالية
        except Exception as e:
            print(f'Error: {e}')
            time.sleep(60)  # الانتظار قبل محاولة جديدة في حالة حدوث خطأ

if __name__ == '__main__':
    main()
