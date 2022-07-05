# warp-plus
使用Github Actions刷取warp+流量

脚本来自ALIILAPRO大佬

## 使用教程
   1.创建一个新库
![image](https://user-images.githubusercontent.com/108753610/177378270-c762f78c-a0ea-4a62-9706-a8d4e9df6ae0.png)
   
   2.新建文件
![image](https://user-images.githubusercontent.com/108753610/177378372-3ee71cba-1960-4a64-9be7-25a353c5047b.png)
   3.复制一下代码并命名为warp.py
   
   其中referrer = str("[#] Enter the WARP+ ID:")改为自己的
   ![image](https://user-images.githubusercontent.com/108753610/177380630-2d0973d7-9be7-4420-9001-7a1f189b9925.png)


   如referrer = str("48118888-8888-8888-8888-917e888887b1")
   ![image](https://user-images.githubusercontent.com/108753610/177378740-99a5e1ee-c003-468c-9d7a-b00976594612.png)

```
import urllib.request
import json
import datetime
import random
import string
import time
import os
import sys
os.system("title WARP-PLUS-CLOUDFLARE By ALIILAPRO")
os.system('cls' if os.name == 'nt' else 'clear')
print('      _______ _      __________________       _______ _______ _______ _______\n'
'     (  ___  | \     \__   __|__   __( \     (  ___  |  ____ |  ____ |  ___  )\n'
'     | (   ) | (        ) (     ) (  | (     | (   ) | (    )| (    )| (   ) |\n'
'     | (___) | |        | |     | |  | |     | (___) | (____)| (____)| |   | |\n'
'     |  ___  | |        | |     | |  | |     |  ___  |  _____)     __) |   | |\n'
'     | (   ) | |        | |     | |  | |     | (   ) | (     | (\ (  | |   | |\n'
'     | )   ( | (____/\__) (_____) (__| (____/\ )   ( | )     | ) \ \_| (___) |\n'
'     |/     \(_______|_______|_______(_______//     \|/      |/   \__(_______)\n')
print ("[+] ABOUT SCRIPT:")
print ("[-] With this script, you can getting unlimited GB on Warp+.")
print ("[-] Version: 4.0.0")
print ("--------")
print ("[+] THIS SCRIPT CODDED BY ALIILAPRO") 
print ("[-] SITE: aliilapro.github.io") 
print ("[-] TELEGRAM: aliilapro")
print ("--------")
referrer = str("[#] Enter the WARP+ ID:")
def genString(stringLength):
	try:
		letters = string.ascii_letters + string.digits
		return ''.join(random.choice(letters) for i in range(stringLength))
	except Exception as error:
		print(error)		    
def digitString(stringLength):
	try:
		digit = string.digits
		return ''.join((random.choice(digit) for i in range(stringLength)))    
	except Exception as error:
		print(error)	
url = f'https://api.cloudflareclient.com/v0a{digitString(3)}/reg'
def run():
	try:
		install_id = genString(22)
		body = {"key": "{}=".format(genString(43)),
				"install_id": install_id,
				"fcm_token": "{}:APA91b{}".format(install_id, genString(134)),
				"referrer": referrer,
				"warp_enabled": False,
				"tos": datetime.datetime.now().isoformat()[:-3] + "+02:00",
				"type": "Android",
				"locale": "es_ES"}
		data = json.dumps(body).encode('utf8')
		headers = {'Content-Type': 'application/json; charset=UTF-8',
					'Host': 'api.cloudflareclient.com',
					'Connection': 'Keep-Alive',
					'Accept-Encoding': 'gzip',
					'User-Agent': 'okhttp/3.12.1'
					}
		req         = urllib.request.Request(url, data, headers)
		response    = urllib.request.urlopen(req)
		status_code = response.getcode()	
		return status_code
	except Exception as error:
		print(error)	

g = 0
b = 0
while True:
	result = run()
	if result == 200:
		g = g + 1
		os.system('cls' if os.name == 'nt' else 'clear')
		print("")
		print("                  WARP-PLUS-CLOUDFLARE (script)" + " By ALIILAPRO")
		print("")
		animation = ["[■□□□□□□□□□] 10%","[■■□□□□□□□□] 20%", "[■■■□□□□□□□] 30%", "[■■■■□□□□□□] 40%", "[■■■■■□□□□□] 50%", "[■■■■■■□□□□] 60%", "[■■■■■■■□□□] 70%", "[■■■■■■■■□□] 80%", "[■■■■■■■■■□] 90%", "[■■■■■■■■■■] 100%"] 
		for i in range(len(animation)):
			time.sleep(0.5)
			sys.stdout.write("\r[+] Preparing... " + animation[i % len(animation)])
			sys.stdout.flush()
		print(f"\n[-] WORK ON ID: {referrer}")    
		print(f"[:)] {g} GB has been successfully added to your account.")
		print(f"[#] Total: {g} Good {b} Bad")
		print("[*] After 18 seconds, a new request will be sent.")
		time.sleep(18)
	else:
		b = b + 1
		os.system('cls' if os.name == 'nt' else 'clear')
		print("")
		print("                  WARP-PLUS-CLOUDFLARE (script)" + " By ALIILAPRO")
		print("")
		print("[:(] Error when connecting to server.")
		print(f"[#] Total: {g} Good {b} Bad")
```
   4.新建workflow
   ![image](https://user-images.githubusercontent.com/108753610/177378837-b9d312a3-bb7b-4ea7-ad89-2f46912c36a8.png)

   5.黏贴以下代码
   
   ![image](https://user-images.githubusercontent.com/108753610/177380834-0639a70c-58b0-45cd-9c4e-f782e2b37a25.png)

   其中corn处可自行修改
```
name: Auto Renew

on:
  workflow_dispatch:
  schedule:
    - cron: 13 */4 * * *
jobs:
  run-it:
    runs-on: ubuntu-latest
    name: Run it on action
    steps:
      - name: Checkout master
        uses: actions/checkout@v2
      - name: setup-python ${{ matrix.pypy }}
        id: setup-python
        uses: actions/setup-python@v3
        with:
          python-version: 3.x
      - name: Setting up
        run:
           python3 wpa.py
```
   6.Enjoy

