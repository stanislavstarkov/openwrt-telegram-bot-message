# openwrt-telegram-bot-message
Send message to telegram from OpenWRT
#Config bot_id and chat_id in UCI
```bash
# cat /etc/config/telegram

config telegram 'bot'
	option bot_id 'your_bot_id'
	option chat_id 'your_chat_id'
```
# Rooter(openwrt mod) customisation
File /usr/lib/sms/smsread.lua was chaged to forward messages to telegram.
Basically only one additional else condition was added:

```lua
   783				if m_r == "0" then
   784					if m_text == "::reboot!!" then
   785						os.execute("(sleep 60; reboot -f) &")
   786					elseif m_text == "::pwrtoggle!!" then
   787						os.execute("(sleep 60; /usr/lib/rooter/pwrtoggle.sh 3) &")
   788					else
   789						os.execute("telegram " .. m_text)
   790					end
   791				end
```
> Remember that file is using Windows carriage return symbols!

Tested in openwrt-19.07 branch (git-20.057.55219-13dd17f) / GoldenOrb_2020-12-05 version
