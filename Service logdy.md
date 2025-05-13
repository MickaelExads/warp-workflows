
## Install Logdy

```warp-runnable-command
sudo curl https://logdy.dev/install-silent.sh | sudo sh
```
## Create a dedicated user to run Logdy[​](https://logdy.dev/docs/logdy-systemd-service#optional-create-a-dedicated-user-to-run-logdy)
```warp-runnable-command
sudo useradd -r -s /bin/false logdy
```
The command above creates a system user named Logdy with no login shell\.
## Systemd file definition[​](https://logdy.dev/docs/logdy-systemd-service#systemd-file-definition)
Next\, we need to create a service definition in a specific location\, open a file with your text editor at the location below\:
```warp-runnable-command
sudo nano /etc/systemd/system/logdy.service
```
and paste the contents below\:
```text
[Unit]
Description=Logdy Socket Listener
After=network.target

[Service]
User=logdy
RuntimeDirectory=logdy
ExecStart=/usr/local/bin/logdy --ui-ip=10.42.0.6 --port=8080 --no-analytics --config=/vagrant/code/logdy.json socket 8000 8001 8002
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target

```
## Enable and run Logdy systemd service[​](https://logdy.dev/docs/logdy-systemd-service#enable-and-run-logdy-systemd-service)
Use the command below to reload systemd so it can pick up a newly added service definition\:
```warp-runnable-command
sudo systemctl daemon-reload
```
Enable Logdy service so it\'s started after a reboot\:
```warp-runnable-command
sudo systemctl enable logdy.service
```
Start the service \(you only have to do it once\)
```warp-runnable-command
sudo systemctl start logdy.service
```
Check the status\:
```warp-runnable-command
sudo systemctl status logdy.service
```
