![Heliactyl](https://cdn.discordapp.com/attachments/881207010417315861/949706607497977976/heliactyl.png)

<hr>

# Heliactyl • The modern client panel for Pterodactyl

All features:
- Resource Management (Use it to create servers, etc)
- Coins (AFK Page earning, Linkvertise earning, Gift them away)
- Renewal (Require coins for renewal)
- Coupons (Gives resources & coins to a user)
- Servers (create, view, edit servers)
- Login Queue (prevent overload)
- User System (auth, regen password, etc)
- Store (buy resources with coins)
- Dashboard (view resources)
- Join for Resources (join discord servers for resources)
- Admin (set/add/remove coins & resources, create/revoke coupons)
- API (for bots & other things)

# Warning

We cannot force you to keep the "Powered by Heliactyl" in the footer, but please consider keeping it. It helps getting more visibility to the project and so getting better. We won't do technical support for installations without the notice in the footer. We may DMCA the website in certain conditions.
Please do keep the footer though.

<hr>

# Install Guide

Warning: You need Pterodactyl already set up on a domain for Heliactyl to work
1. Upload the file above onto a Pterodactyl NodeJS server [Download the egg from Parkervcp's GitHub Repository](https://github.com/parkervcp/eggs/tree/master/bots/discord/discord.js)
2. Unarchive the file and set the server to use NodeJS 16
3. Configure settings.json (specifically panel domain/apikey and discord auth settings for it to work)
4. Start the server (Ignore the 2 strange errors that might come up)
5. Login to your DNS manager, point the domain you want your dashboard to be hosted on to your VPS IP address. (Example: dashboard.domain.com 192.168.0.1)
6. Run `apt install nginx && apt install certbot` on the vps
7. Run `ufw allow 80` and `ufw allow 443` on the vps
8. Run `certbot certonly -d <Your Heliactyl Domain>` then do 1 and put your email
9. Run `nano /etc/nginx/sites-enabled/heliactyl.conf`
10. Paste the configuration at the bottom of this and replace with the IP of the pterodactyl server including the port and with the domain you want your dashboard to be hosted on.
11. Run `systemctl restart nginx` and try open your domain.

# Nginx Proxy Config
```Nginx
server {
    listen 80;
    server_name <domain>;
    return 301 https://$server_name$request_uri;
}
server {
    listen 443 ssl http2;
location /afkwspath {
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
  proxy_pass "http://localhost:<port>/afkwspath";
}
    
    server_name <domain>;
ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
location / {
      proxy_pass http://localhost:<port>/;
      proxy_buffering off;
      proxy_set_header X-Real-IP $remote_addr;
  }
}
```

<hr>

# Additional Configuration

Enabling other eggs (Minecraft Bedrock):
1. [Download the eggs from Parkervcp's GitHub Repository](https://github.com/parkervcp/eggs/tree/master/bots/discord/discord.js)
2. Add the Pocketmine & Vanilla Bedrock eggs to your panel
3. Get the egg ID of both of them and set it as the ID in settings.json

# Updating 

From Heliactyl v11 or Dashactyl v0.4 to Heliactyl v12:
1. Store certain things such as your api keys, discord auth settings, etc in a .txt file
2. Download database.sqlite 
3. Delete all files off the server (or delete and remake the folder if done in ssh)
4. Upload the latest Heliactyl v12 release and unzip it
5. Upload database.sqlite and reconfigure settings.json

Move to a newer Heliactyl v12 release:
1. Delete everything except settings.json, database.sqlite
2. Put the files that you didn't delete into a zip file
3. Upload the latest Heliactyl v12 release and unzip it
4. Remove settings.json and database.sqlite
5. Unzip the zip with your old settings.json and database.sqlite

# Running In Background And on Startup
Installing [pm2](https://github.com/Unitech/pm2):
- Run `npm install pm2 -g` on the vps

Starting The Dashboard in Background:
- Change directory to your Heliactyl Files Using `cd` command, 
Example:- `cd /home/user/dash-files` 
- To Start The App, Run `pm2 start index.js --name "heliactyl"`
- To View Logs, Run `pm2 logs heliactyl`

Making the Dashboard Run on Startup:
- Make Sure Your Dashboard is running in the background with the help of [pm2](https://github.com/Unitech/pm2)
- You can check if your app is running in background with `pm2 list`
- Once You Confirmed That your app us running in background, You Can Generate Startup script by
  Running `pm2 startup` and `pm2 save`
- Note: Supported Init Systems are `systemd`, `upstart`, `launchd`, `rc.d`
- To Remove Your Dashboard Running on Startup, Run `pm2 unstartup`

To Stop The Dashboard Which is running in background, Use `pm2 stop heliactyl`
# Legacy Deprecation Notice

Heliactyl v6, v7, v8, v9, v10, v11 is now deprecated as listed in our Discord and should not be used.
Please update to Heliactyl v12.


