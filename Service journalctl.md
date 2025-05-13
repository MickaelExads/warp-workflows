## Systemd file definition[​](https://logdy.dev/docs/logdy-systemd-service#systemd-file-definition)
Next\, we need to create a service definition in a specific location\, open a file with your text editor at the location below\:
```warp-runnable-command
sudo nano /etc/systemd/system/logdy-journalctl.service
```
and paste the contents below\:
```code
[Unit]
Description=Forward php-fpm Journal to Logdy
After=logdy.service

[Service]
User=root
ExecStart=/bin/bash -c 'exec journalctl -u php-fpm -f -o json | logdy forward 8000'
Restart=on-failure

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
sudo systemctl enable logdy-journalctl.service
```
Start the service \(you only have to do it once\)
```warp-runnable-command
sudo systemctl start logdy-journalctl.service
```
Check the status\:
```warp-runnable-command
sudo systemctl status logdy-journalctl.service
```
