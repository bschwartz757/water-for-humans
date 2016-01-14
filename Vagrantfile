# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

  config.vm.box = "hashicorp/precise32"

  config.vm.network "forwarded_port", guest: 80, host: 8282 #HTTP
  config.vm.network "forwarded_port", guest: 3306, host: 3309 #MySQL
  # config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder "./www", "/var/www", create: true, :mount_options => ["dmode=777", "fmode=666"]

  config.vm.provision "shell", inline: <<-SHELL

    #install software
    debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    echo "Updating software listings..."
    sudo apt-get update -qq
    echo "Installing software from repositories..."
    sudo apt-get install apache2 mysql-server php5 php5-mysql git curl -y -q

    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer
    chmod 777 /usr/local/bin/composer

    #create database
    echo "Creating MySQL database..."
    mysql -u root --password='root' --execute='CREATE DATABASE IF NOT EXISTS wordpress;'

    #add the `vagrant` user to the www-group
    sudo adduser vagrant www-data

    #download and install WordPress
    echo "Downloading and installing WordPress"
    cd /var/www
    curl -s https://wordpress.org/latest.tar.gz | tar xz --strip-components=1
    mv index.html _index.html

    #restart Apache (sometimes it doesn't see PHP's MySQL adapter)
    sudo /etc/init.d/apache2 restart

    SHELL

  config.vm.post_up_message = <<-POSTUP

Your virtual machine is now up and running. 

To pause this VM, use the `vagrant halt` command.

To resume it, use `vagrant up`.

Visit http://localhost:8080 to visit your local server. Web files are located in the www/ folder in this directory. They will not be erased when you halt or restart the server, and you can edit them using a normal desktop editor. You can also clone your theme into www/wp-content/themes to work on it.

MySQL config info for WordPress:
  Database name: wordpress
  User name: root
  Password: root
  Database host: localhost
  Table Prefix: wp_

  POSTUP
end