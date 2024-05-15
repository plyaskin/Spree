# Spree Starter

This is a starter kit for [Spree Commerce](https://spreecommerce.org) - the open-source e-commerce platform for Rails. It is a great starting point for any Rails developer to quickly build an e-commerce store.

This starter uses:

* Spree Commerce 4.8 which includes Admin Dashboard, API and Storefront
* Ruby 3.3 and Ruby on Rails 7.1
* Solid Queue with Mission Control UI (access only to Spree admins) for background jobs
* Solid Cache for excellent caching and performance

You don't need to install any additional tools or libraries to start developing with Spree Starter. Everything is already set up for you.

## Installation

Make sure you have the following installed:
* Docker with Docker Compose - [installation instructions](https://docs.docker.com/get-docker/)
* Ruby 3.3 - [installation instructions](https://www.ruby-lang.org/en/documentation/installation/)
* Vips - [installation instructions](https://libvips.github.io/libvips/install.html)

```bash
bin/setup
```

If you want to use sample data (products, categories), you can load it using the following command:

```bash
bin/rake spree_sample:load
```

### Switching to MySQL

By default, Spree Starter uses PostgreSQL. If you want to switch to MySQL, you can do so by running the following command:

```bash
bin/rails db:system:change --to=mysql
```

You will also need to run `bin/setup` again to install the MySQL adapter and create the database.

### Launch local server

```bash
bin/rails s
```

## Deployment

### Using Render

<a href="https://render.com/deploy?repo=https://github.com/spree/spree_starter/tree/main">
  <img src="https://render.com/images/deploy-to-render-button.svg" alt="Deploy to Render" height=32>
</a>

Note that sample data does not automatically get loaded when deploying to Render with the default configuration. In order to add sample data, run the following commands in the web service shell:

```bash
bin/rake spree_sample:load
```

### Using Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

### Other platforms

Spree Starter is a standard Rails application, so you can deploy it to any platform that supports Ruby on Rails applications. You can also use Docker to deploy it to any container-based platform. Please check [Spree Guides](https://guides.spreecommerce.org/developer/deployment.html) for more information.

## Troubleshooting

### libvips error

If you encounter an error like the following:

```bash
LoadError: Could not open library 'vips.so.42'
```

Please check that libvips is installed with `vips -v`, and if it is not installed, follow [installation instructions here](https://www.libvips.org/install.html).

## Commands list
```bash
# Git clone
git clone https://github.com/plyaskin/Spree sajm.wedtp.com

# Redis
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list

sudo apt-get update
sudo apt-get install redis -y
sudo systemctl enable redis-server.service
sudo systemctl start redis-server.service

# PostgreSQL
sudo apt install postgresql -y

# Add Docker's official GPG key:
sudo apt-get update -y
sudo apt-get install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Ruby 3.3.0
# sudo apt-get install ruby-full -y
sudo apt install gnupg2
gpg2 --keyserver hkp://keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
\curl -sSL https://get.rvm.io -o rvm.sh
cat rvm.sh
curl -L https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install ruby 3.3.0
sudo ln -s /var/www/plyaskin/data/.rvm/rubies/ruby-3.3.0/bin/ruby /usr/bin/ruby
sudo ln -s /var/www/plyaskin/data/.rvm/rubies/ruby-3.3.0/bin/gem /usr/bin/gem
sudo ln -s /var/www/plyaskin/data/.rvm/gems/ruby-3.3.0/bin/bundle /usr/local/bin/bundle

# Vips
sudo apt install libvips -y
sudo apt install libvips-tools -y

# NodeJS
sudo apt-get install nodejs -y

sudo apt install docker-compose -y
# sudo docker-compose up

sudo /etc/init.d/redis-server stop
sudo /etc/init.d/postgresql stop

sudo apt install postgresql-contrib libpq-dev
gem install bundler
gem update --system 3.5.10

bundle install
gem install bummr

## Other stupid actions
# Change "port = " to other, ex. 5432 to 5439 and 6739 to 6732
sudo nano /etc/postgresql/14/main/postgresql.conf
sudo nano /etc/redis/redis.conf


sudo bin/setup
```
