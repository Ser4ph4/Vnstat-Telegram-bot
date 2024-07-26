# Vnstat-Telegram-bot
BOT for VNSTAT
==============================================

1,You have to apply a telegram bot@BotFather
2,You will get your chat id and token to access the http api
curl -k --data chat_id="chat id" --data "text=This is a test message" "https://api.telegram.org/bot:<Your bot token>/sendMessage"

3,install vnstat and vnstati and config it.

apt install vnstat vnstati

config default ethernet number

nano /etc/vnstat.conf (normally it is eth0)

4,Create a script and make it run everyday.

touch /path/to/vnstattotg.sh
nano /path/to/vnstattotg.sh

copy and paste below:


(title="*`hostname` - Everyday traffic usage*"

vnstati -s -o <path to today.png>

curl -X POST \
    -H "Content-Type: application/json" \
    -d "{\"chat_id\": \"<Your chat id>\", \"text\": \"${title}\", \"parse_mode\": \"Markdown\"}" \
    https://api.telegram.org/bot<Your bot token>/sendMessage

curl -F "chat_id=<Your chat id>" \
    -F "caption=\"Everyday traffic usage\"" \
    -F "photo=@/<path to today.png>" \
    https://api.telegram.org/bot<Your bot token>/sendPhoto)

Give it a correct permission

chmod +x /path/to/vnstattotg.sh

crontab -e
0 0 * * * /bin/bash /path/to/vnstattotg.sh (run everyday at 00:00)

Enjoy!
