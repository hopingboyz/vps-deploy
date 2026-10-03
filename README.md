`git clone https://github.com/hopingboyz/vps-deploy`

cd vps-deploy

cp test.env .env

apt install python3-pip -y

mkdir -p ~/.config/pip && echo -e "[global]\nbreak-system-packages = true" > ~/.config/pip/pip.conf

pip install -r requirements.txt

sudo nano /etc/systemd/system/unixbot.service

[Unit]
Description=UnixBot Discord Bot
After=network.target

[Service]
User=root
WorkingDirectory=/root
ExecStart=/usr/bin/python3 /root/bot.py
Restart=always
RestartSec=5
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl restart unixbot
