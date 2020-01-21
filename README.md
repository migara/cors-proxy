# cors-proxy

## Install Node.js
yum install -y gcc-c++ make  
curl -sL https://rpm.nodesource.com/setup_12.x | sudo -E bash -  
sudo yum install nodejs  

## Install git
sudo yum install git  

## Setup CORS proxy server
cd ~  
git clone https://github.com/migara/cors-proxy.git  
cd cors-proxy  
npm install  
vi server.js, update targetURL variable to SNOW URL on line  

## Install PM2 process manager 
npm i -g pm2  
pm2 start server.js  
pm2 startup  
// pm2 reload server (optional)  

## Install Nginx
yum install nginx  
cp ~/cors-proxy/nginx_conf/cors.conf /etc/nginx/conf.d  
sudo systemctl enable nginx  
sudo systemctl start nginx  
sudo systemctl status nginx  
// sudo systemctl restart nginx  

setsebool -P httpd_can_network_connect 1  
semanage port -l | grep http_port_t  
semanage port -a -t http_port_t  -p tcp 8080  

##(Optional) 
Nginx access logs  
tail -f /var/log/nginx/access.log  

Nginx error logs  
tail -f /var/log/nginx/error.log  








