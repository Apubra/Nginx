# Nginx
Install in Linux-
sudo apt install nginx

sudo nano /etc/nginx/sites-available/default

Default settings:
server {
    server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:5000; #whatever port your app runs on
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

# Check NGINX config
sudo nginx -t

# Restart NGINX
sudo service nginx restart

# Reverse Proxy for many domains(IP)
Next, you’ll want to make an Nginx configuration file for each of your domain(IP) in the /etc/nginx/sites-available directory.

site1.conf
site2.conf
(your_domain.conf)

Publish your websites by making a symlink from your Nginx configuration files to the sites-enabled directory.

sudo ln -s /etc/nginx/sites-available/site1.conf /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site2.conf /etc/nginx/sites-enabled/

Finally, test your Nginx configuration changes and restart the web server.

nginx -t
systemctl restart nginx

You can get an error. Because of maybe your port 80 already running.
So, run the following command:
sudo fuser -k 80/tcp
sudo fuser -k 443/tcp

Then execute,
sudo service nginx restart
