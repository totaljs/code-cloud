# Total.js: Code Cloud

- [Documentation](https://docs.totaljs.com)
- [Join Total.js Telegram](https://t.me/totaljs)
- [Support](https://www.totaljs.com/support/)

__Instructions__:

- target DNS of your domains to your server
- install docker
- clone on your server https://github.com/evertramos/nginx-proxy-automation
	- update `nginx.tmpl` in the Tune NGINX section
	- follow step 1
	- `cd proxy/bin`
	- `fresh-start.sh --yes -e your_email@domain --skip-docker-image-check --use-nginx-conf-files`
- install Node.js
- make `/www/www/` directory
- make `/www/node_modules/` directory
- install `$ npm install total4`
- then clone this project
- edit `docker-compose.yaml`
- run `docker compose up -d`


## Tune NGINX

### Disable access logging

- update `/www/proxy/nginx.tmpl` file

```bash
# REPLACE:
{{ $access_log := (or (and (not $.Env.DISABLE_ACCESS_LOGS) "access_log /var/log/nginx/access.log vhost;") "") }}

# TO:
{{ $access_log := "" }}
```

### Set specific NGINX settings for domain

Just create a text file with NGINX your configuration. The file below is appended before `location / {`:

```
/www/proxy/data/vhost.d/yourdomain.com
/www/proxy/data/vhost.d/subdomain.yourdomain.com
/www/proxy/data/vhost.d/default             --> for all domains
```

The file below is appended into the `location / {`:

```
/www/proxy/data/vhost.d/yourdomain.com_location
/www/proxy/data/vhost.d/subdomain.yourdomain.com_location
/www/proxy/data/vhost.d/default_location    --> for all domains
```

---

We recommend merging the `proxy` folder with the `nginx-proxy-automation` folder for extending NGINX configuration.