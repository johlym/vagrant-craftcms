# -*- mode: ruby -*-
# vi: set ft=ruby :

# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty32"
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "private_network", ip: "11.22.33.44"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end
  config.vm.provision "file", source: "craftcms.conf", destination: "craftcms.conf"
  config.vm.provision "shell", inline: <<-SHELL
    echo UPDATING SYSTEM...
    sudo apt-get update
    echo PREPARING FOR MYSQL...
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    echo INSTALLING SOFTWARE...
    sudo apt-get install -y vim curl python-software-properties mysql-server nginx php5-fpm php5-mysql imagemagick php5-imagick php5-curl
    sudo sed -i "s/^bind-address/#bind-address/" /etc/mysql/my.cnf
    sudo service mysql restart
    sudo mysql -u root -proot -e "CREATE DATABASE craft;"
    sudo mysql -u root -proot -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION; FLUSH PRIVILEGES;"
    sudo service mysql restart
    sudo /etc/init.d/mysql restart
    sudo rm /etc/php5/fpm/php.ini
    sudo cp /vagrant/php.ini /etc/php5/fpm/php.ini
    sudo php5enmod mcrypt
    sudo service php5-fpm restart
    sudo cat /vagrant/craftcms.conf | sudo tee /etc/nginx/sites-available/default
    sudo service nginx restart
    sudo mkdir /var/www
    sudo mkdir /var/www/craftcms
    sudo cp -R /vagrant/craft/public /var/www/craftcms/
    sudo cp -R /vagrant/craft/craft /var/www/craftcms/
    sudo cat /vagrant/db.php | sudo tee /var/www/craftcms/craft/config/db.php
    sudo chmod 0777 /var/www/craftcms/craft/app
    sudo chmod 0777 /var/www/craftcms/craft/config
    sudo chmod 0777 /var/www/craftcms/craft/storage
    echo DONE.
    echo ACCESS VIA HTTP://11.22.33.44.
  SHELL
end
