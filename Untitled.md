

```text
bash -c 'journalctl -u php-fpm.service -f -o cat & tail -n 20 /var/exads/log/e738bad9/campaigns-caching-v3.php.output.log | sed "s/^/[campaigns-caching] /" & tail -n 20 /var/exads/log/e738bad9/campaigns-caching-v3-push.php.output.log | sed "s/^/[campaigns-caching-push] /"' | logdy --ui-ip=10.42.0.6 --port=80 --no-analytics --config /vagrant/code/logdy.json
```
