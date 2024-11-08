
def detect_pattern(data):
    # Example logic to detect Hammer candlestick
    if data['Close'] > data['Open'] and \
        (data['Close'] - data['Open']) < (data['High'] - data['Low']) * 0.25:
        return "Hammer"
    return None
from telegram.ext import Updater, CommandHandler

def signal(update, context):
    market_data = fetch_market_data()  # Function to fetch market data
    pattern = detect_pattern(market_data)
    if pattern:
        update.message.reply_text(f"Signal: {pattern} detected!")
    else:
        update.message.reply_text("No reliable signal at the moment.")

# Set up bot
updater = Updater("7561233787:AAHOW6EUfkrCwcHHkIlYnQPLJAl0rqN1Hkc", use_context=True)
dp = updater.dispatcher
dp.add_handler(CommandHandler("signal", signal))
updater.start_polling()
updater.idle()
