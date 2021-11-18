# BASH-script-3commas
#t-bot-manager v.0.0.3
#Be sure you have a DCA Bot setup on 3commas with Tradingview Custom Alerts
#!/bin/bash
echo "Enter Bot Alias"
read al
echo "Enter Bot ID"
read id
echo "Enter Email Token"
read et
echo "3commas Webhook"
read 3c

#Command Definition

command1="curl -X POST $3c -H \"Content-Type: application/json\" -d \"{\\\"action\\\": \\\"start_bot_and_start_deal\\\", \\\"message_type\\\": \\\"bot\\\", \\\"bot_id\\\": $id, \\\"email_token\\\": \\\"$et\\\", \\\"delay_seconds\\\": 0}\""

command2="curl -X POST https://3commas.io/trade_signal/trading_view -H \"Content-Type: application/json\" -d \"{\\\"action\\\": \\\"close_at_market_price_all_and_stop_bot\\\", \\\"message_type\\\": \\\"bot\\\", \\\"bot_id\\\": $id, \\\"email_token\\\": \\\"$et\\\", \\\"delay_seconds\\\": 0}\""

#Make a folder for the bot
mkdir -p /home/$USER/t-bot-mannager/$al/

#Write start bot and deal
echo "#!/bin/bash" >> /home/$USER/t-bot-mannager/$al/start-$al.sh
echo "$command1" >> /home/$USER/t-bot-mannager/$al/start-$al.sh

#Give permitions to the new scrip
chmod +x /home/$USER/t-bot-mannager/$al/start-$al.sh

#Test to see if bot activates and starts the deal 
echo "Do you want to start the bot and deal? yes/no"
read n
if [[  $n == "yes" ]]
then
    echo 'Executing bot ...'
    exec /home/$USER/t-bot-mannager/$al/start-$al.sh
else
echo "Do you want a start/stop script for your bot? yes/no"
read ss

if [[  $ss == "yes" ]]
then
        echo "#!/bin/bash" >> /home/$USER/t-bot-mannager/$al/stop-$al.sh
        echo "$command2" >> /home/$USER/t-bot-mannager/$al/stop-$al.sh
        chmod +x /home/$USER/t-bot-mannager/$al/start-$al.shstop-$al.sh
else
        echo "Bye"
