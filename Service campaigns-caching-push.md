## Systemd file definition[​](https://logdy.dev/docs/logdy-systemd-service#systemd-file-definition)
Next\, we need to create a service definition in a specific location\, open a file with your text editor at the location below\:
```warp-runnable-command
sudo nano /etc/systemd/system/logdy-campaigns-caching-push.service
```
and paste the contents below\:
```code
[Unit]
Description=Forward Exads PHP logs to Logdy
After=logdy.service

[Service]
User=logdy
ExecStart=/bin/bash -c 'exec tail -f /var/exads/log/e738bad9/campaigns-caching-v3-push.php.output.log | logdy forward 8002'
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
## Enable and run service[​](https://logdy.dev/docs/logdy-systemd-service#enable-and-run-logdy-systemd-service)
Use the command below to reload systemd so it can pick up a newly added service definition\:
```warp-runnable-command
sudo systemctl daemon-reload
```
Enable Logdy service so it\'s started after a reboot\:
```warp-runnable-command
sudo systemctl enable logdy-campaigns-caching-push.service
```
Start the service \(you only have to do it once\)
```warp-runnable-command
sudo systemctl start logdy-campaigns-caching-push.service
```
Check the status\:
```warp-runnable-command
sudo systemctl status logdy-campaigns-caching-push.service
```
