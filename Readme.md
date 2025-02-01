
## 🍁Nginx Reverse proxy server setup

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
        [![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue)](https://www.linkedin.com/in/nikhil--chaudhari/)
        [![Medium](https://img.shields.io/badge/Medium-Writeups-black)](https://medium.com/@nikhil-c)


## 🍁Introduction 
In this project, I am going to setup 2 apache web server that are attack to nginx reverse proxy server. Lets start step by step.

![](https://github.com/DNcrypter/Reverse-Proxy-Server-setup/blob/main/images/img2.png)
## 🍁 Nginx web server setup :
As Nginx is available in Ubuntu’s default repositories, it is possible to install it from these repositories using the **apt** packaging system:
### Step 1 - Installing Nginx
```
sudo apt update
sudo apt install nginx
```
### Step 2 - Adjusting the Firewall
enable required profile by typing and also verify the changes:
```
sudo ufw allow 'Nginx HTTP'
sudo ufw status
```
The output will indicated which HTTP traffic is allowed:

### Step 3 - Checking your Web Server
```
systemctl status nginx

http://your_server_ip:8080
```
![](https://github.com/DNcrypter/Reverse-Proxy-Server-setup/blob/main/images/img4.png)
Now you have successfully setup nginx server.  
### Refer Nginx web server setup my medium post
[www.medium.com/how-to-setup-nginx-web-server](https://medium.com/@nikhil-c/how-to-setup-nginx-web-server-on-ubuntu-v20-39ec20c0dbc3)


## 🍁 Apache Web server setup
As I have already setup 2 apache web servers required to link nginx reverse proxy with it in my medium blog :
[www.medium.com/how-to-install-the-apache-web-server](https://medium.com/@nikhil-c/how-to-install-the-apache-web-server-with-proxy-setup-on-ubuntu-v20-8a2cf4a0891f)

## 🍁 Nginx Reverse proxy server Configuration
As we setup already setup 2 apache2 web server and 1 nginx server which act as reverse proxy after we configure it. So lets configure:

#### Check all three required service status :
```
systemctl status httpd.service
systemctl status nginx.service
systemctl status firewalld.service
```

#### check normal working :
* check apache server : http://my-ip:80/index.html
* check nginx server : http://my-ip:8080/
![](https://github.com/DNcrypter/Reverse-Proxy-Server-setup/blob/main/images/img3.png)
![](https://github.com/DNcrypter/Reverse-Proxy-Server-setup/blob/main/images/img4.png)
Yes, both are working.

#### edit config file :
/etc/nginx/nginx.conf
```
location / {
        proxy_pass http://my-ip:8080/;
}
```
#### To Restrict public access of secret.html file
```
location /secret.html {
        deny all;
        return "403 Forbidden";
    }
```
* Test the configuration for syntax errors.
* If the test is successful, reload Nginx to apply the changes:
```
sudo nginx -t
sudo systemctl reload nginx
```

* After setup whole configuration just start and stop the service to reload all changes :
```
systemctl stop nginx.service
systemctl start nginx.service
```

#### Final working check 
* Browser nginx server : http://my-ip:8080/

![](https://github.com/DNcrypter/Reverse-Proxy-Server-setup/blob/main/images/img4.png)

* It reflects with apache server default page. It means, we successfully setup reverse proxy.

## 🍁 Conclusion 
At starting, we setup nginx server then apache server after that we configured reverse proxy setting and firewall setting to allow proxy traffic. 
