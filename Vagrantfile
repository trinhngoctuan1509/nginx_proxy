proxy_ip  = "192.168.0.30"
backend_ip  = "192.168.0.31"

proxy_script = 
"
sudo su -
mv /etc/nginx/conf.d/proxy.petshoptomandjerry.com.conf /etc/nginx/conf.d/proxy.petshoptomandjerry.com
apt update
apt install nginx -y
rm /etc/nginx/sites-enabled/default
rm /etc/nginx/sites-available/default
rm -r /var/www/html
mv /etc/nginx/conf.d/proxy.petshoptomandjerry.com /etc/nginx/conf.d/proxy.petshoptomandjerry.com.conf
systemctl reload nginx
"

backend_script = 
"
sudo su -
mv /etc/nginx/conf.d/backend.petshoptomandjerry.com.conf /etc/nginx/conf.d/backend.petshoptomandjerry.com
apt update
apt install nginx -y
rm /etc/nginx/sites-enabled/default
rm /etc/nginx/sites-available/default
rm -r /var/www/html
mv /etc/nginx/conf.d/backend.petshoptomandjerry.com /etc/nginx/conf.d/backend.petshoptomandjerry.com.conf
mkdir /var/www/petshoptomandjerry.com
cd /var/www/petshoptomandjerry.com
echo 'Day that su la noi dung cua BE tom&jerry' > /var/www/petshoptomandjerry.com/index.html
systemctl reload nginx
"

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.define "proxy" do |proxy|
    proxy.vm.network "private_network", ip: proxy_ip
    proxy.vm.provision "shell", inline: proxy_script
    proxy.vm.synced_folder "./proxy_conf.d", "/etc/nginx/conf.d"
  end
 
  config.vm.define "backend" do |server|
    server.vm.network "private_network", ip: backend_ip
    server.vm.provision "shell", inline: backend_script
    server.vm.synced_folder "./backend_conf.d", "/etc/nginx/conf.d"
  end
end
