#How to run#

* Change server locale: add LC_ALL="en_US.utf-8" to /etc/environment (or ru_RU.utf-8)
* bundle exec knife solo prepare root@appserver1.riskgap.com
* bundle exec knife solo cook root@104.236.220.145 (in chef-repo directory)
* Make environment fix ups (see below)
* bundle exec cap production deploy (in project directory)

#Installation fix ups#

* rbenv global 2.0.0-p598

#Configure Postgres#

Note: postgres steps doesn't needed if you install locally

* Change postgres config: https://www.digitalocean.com/community/tutorials/scaling-ruby-on-rails-setting-up-a-dedicated-postgresql-server-part-3:

##/etc/postgresql/9.3/main/postgresql.conf##

```
#!bash

#listen_addresses = 'localhost'
#Change it to:

listen_addresses = '*'

```

##/etc/postgresql/9.3/main/pg_hba.conf##

After the comment block, append the following line:

```
#!bash

# TYPE   DATABASE      USER        ADDRESS        METHOD
host        all        all        0.0.0.0/0        md5
```

* service postgresql restart
* Capistrano script
* export RAILS_ENV=production;bundle exec rake db:seed (run if you installing into new database)

# Known issues #

* Environment variables are not read from config.

##Ubuntu ssh agent issues troubleshooting## 

You need to call:

```
#!bash

eval "$(ssh-agent)"
ssh-add ~/.ssh/id_rsa
```

## Errbit ##

* email:    errbit@errbit.example.com
* password: BJdrcP5zyD9r