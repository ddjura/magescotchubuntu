# TODO 
-  install sample data for magento 2


# MageScotch Box

This is the PHP 7-based version of Magescotch. 

This environment is based on the Vagrant base box Magemalt. 

Magescotch is designed to allow you to experiment with Magento. While sample installations of M2 is setup for you, the main purpose of the environment is to give you a place to work on your own projects.

Magescotch is built for general purpose use, but began with conferences and training sessions in mind. Because of how dodgy conference wifi can be, we include any tool we think you might need in the Magescotch base box. When in doubt, poke around /usr/local/src/ for lots of preloaded goodies. The Composer cache is also prewarmed with a number of Magento-related libraries. This makes Magescotch also especially useful on planes, trains and other situations with little-to-no bandwidth available. 


## Get Started
- Download and Install [Vagrant][3] - please make sure you are running the latest version of Vagrant. 1.8.7 or newer. 
- Download and Install [VirtualBox][4] - please make sure you are running the latest version of VirtualBox. 5.1.0 or newer.
- Install the Vagrant plugins required by running: vagrant plugin install vagrant-hostmanager vagrant-auto_network
- Clone the this MageScotch Ubuntu Box [GitHub Repository](https://github.com/ddjura/magescotchubuntu) or Download ZIP if you don't want to contribute to the repo
- Edit local-bootstrap.sh and replace the name and email address with your information and desired admin user
- Run `vagrant up` (ON windows run `vagrant up --provider virtualbox`
- Move out magento cron jobs from root cron tab into vagrant user crontab and set permission again (see Issues section) 
- Access Magento 2 at [http://192.168.33.10/magento2/](http://192.168.33.10/magento2/)
- Access Magento 2 backend at [http://192.168.33.10/magento2/adminpanel](http://192.168.33.10/magento2/)
- magento 2 sample code git repo is here [https://github.com/ddjura/Magento2Sample]
- Use your favorite IDE to edit the files in public/magento2
- Access Mailcatcher at [http://192.168.33.10:1080/](http://192.168.33.10:1080/)
- Access phpmyadmin at [http://192.168.33.10/phpmyadmin/](http://192.168.33.10/phpmyadmin/)
- Access adminer at [http://192.168.33.10/adminer/](http://192.168.33.10/adminer/)



## Issues
Some common issues listed here, if you have more questions please contact me at ddjura87@gmail.com or trough my website www.markodurasic.com :
- If permission issues then reference this:
http://devdocs.magento.com/guides/v2.0/install-gde/prereq/file-system-perms.html


- If memory used up by pending cronjob,that is because the email are trying to be sent but the email server is not set, so pending jobs would ba accumuluated..Temporary solution which os ok for local environemnt would be adding this to crontab as file system user:
*/2 * * * * /usr/bin/mysql -u dev -pdev -e "truncate magento2.cron_schedule"

- Cron tab permission issues, by default the root cron tab is set for magento cron jobs, so move it out of the root cron tab into vagrant user cron tab. As vagrant is the file system owner.

## Common Tasks

### Add SSH keys to SSH agent so the Vagrant box can use them via SSH agent forwarding

This only works on Mac and Linux host machines, but on those OS's, on your local machine, run:

ssh-add <path to the private key you want to use in the Vagrant box>

Make sure that your ~/.ssh/config file on your local machine includes these lines:

Host                    *
ForwardAgent          yes 

Troubleshoot issues by making sure SSH is aware of your key, by running:

ssh-add -l

## Credentials

### Databases / MySQL

Username: dev
Password: dev
Databases: magento, magento2, dev

### Admin accounts
- Magento 1: http://192.168.33.10/magento1/admin_dev/ username: admin password: 64-solution-DISH-into-64
- Magento 2: http://192.168.33.10/magento2/admin_dev/ username: admin password: 64-solution-DISH-into-64

## Common Issues

## Features
### System Stuff
- Ubuntu 1.04 LTS 
- PHP 7.0 
- Ruby 2.2.x
- Vim
- Git
- cURL
- GD and Imagick
- Composer
- Beanstalkd
- Node
- NPM
- Mcrypt
- Mailcatcher
- Z-Ray

### Magento Stuff
- Magento 2 ([http://192.168.33.10/magento2/](http://192.168.33.10/magento2/)) - files in public/magento2

### Database Stuff
- MySQL
- PostgreSQL
- SQLite

### Caching Stuff
- Redis
- Memcache and Memcached

### Node Stuff
- Grunt
- Bower
- Yeoman
- Gulp
- Browsersync
- PM2

### Laravel Stuff
- Laravel Installer
- Laravel Envoy
- Blackfire Profiler

### Other Useful Stuff
- No Internet connection required
- PHP Errors turned on
- Laravel and WordPress ready
- Operating System agnostic
- Goodbye XAMPP / WAMP
- New Vagrant version? Update worry free. ScotchBox is very reliable with a lesser chance of breaking with various updates
- Super easy database access and control
- [Virtual host ready](https://scotch.io/bar-talk/announcing-scotch-box-2-0-our-dead-simple-vagrant-lamp-stack-improved#multiple-domains-(virtual-hosts))
- PHP short tags turned on
- H5BP's server configs
- MIT License

## Basic Vagrant Commands
### Start or resume your server

```bash
vagrant up
```

### Pause your server

```bash
vagrant suspend
```

### Delete your server

```bash
vagrant destroy
```

### SSH into your server

```bash
vagrant ssh
```

## Database Access
### MySQL
- Hostname: localhost or 127.0.0.1
- Username: root
- Password: root
- Database: scotchbox

### PostgreSQL
- Hostname: localhost or 127.0.0.1
- Username: root
- Password: root
- Database: scotchbox
- Port: 5432

## SSH Access
- Hostname: 127.0.0.1:2222
- Username: vagrant
- Password: vagrant

## Updating the Box
Although not necessary, if you want to check for updates, just type:

```bash
vagrant box outdated
```

It will tell you if you are running the latest version or not, of the box. If it says you aren't, simply run:

```bash
vagrant box update
```

## Setting a Hostname
If you're like me, you prefer to develop at a domain name versus an IP address. If you want to get rid of the some-what ugly IP address, just add a record like the following example to your computer's host file.

```bash
192.168.33.10 whatever-i-want.local
```

Or if you want "www" to work as well, do:

```bash
192.168.33.10 whatever-i-want.local www.whatever-i-want.local
```

Technically you could also use a Vagrant Plugin like [Vagrant Hostmanager][15] to automatically update your host file when you run Vagrant Up. However, the purpose of Scotch Box is to have as little dependencies as possible so that it's always working when you run "vagrant up".

## Scotch Box
MageScotch Box is based on Scotch Box v2 - [https://github.com/scotch-io/scotch-box](https://github.com/scotch-io/scotch-box)

Learn more about Scotch Box v2:

### Check out the official docs at: [box.scotch.io][16]
### [Read the getting started article](https://scotch.io/bar-talk/introducing-scotch-box-a-vagrant-lamp-stack-that-just-works)
### [Read the 2.0 release article](https://scotch.io/bar-talk/announcing-scotch-box-2-0-our-dead-simple-vagrant-lamp-stack-improved)
![Scotch Box](https://cask.scotch.io/2015/07/scotch-box-2.png)

Scotch Box is a preconfigured Vagrant Box with a full array of LAMP Stack features to get you up and running with Vagrant in no time.

A lot of PHP websites and applications don't require much server configuration or overhead at first. This box should have all your needs for doing basic development so you don't have to worry about configuring Vagrant and you can simply focus on your code.

No provisioning tools or setup is really even required with Scotch Box. Since everything is packaged into the box, running "vagrant" is super fast, you'll never have to worry about your environment breaking with updates, and you won't need Internet to code.

![Scotch Box](https://cask.scotch.io/2015/07/Screen-Shot-2015-07-15-at-10.49.17-AM.png)

### What and Why
Vagrant is an extremely powerful tool. With Chef or Puppet and Vagrant, you can configure any type of server environment you can think of. The possibilities are endless (especially with Docker in the picture now, too). Speaking candidly though, most the development I do doesn't really stray from a default LAMP stack, and when I have to configure a server, I really am always just setting up a boring typical LAMP stack anyways. **All I really want is PHP 5.6 and a bunch of modules with zero hassle or overhead**.

I used to use this seriously awesome [Vagrant LAMP Stack][1] that I even wrote about [here][2]. The problem with this is it broke a lot. It broke when Vagrant updated, it broke when Chef updated, and it broke when Berkshelf updated. On top of that, I always had problems getting it working on Windows. There are just too many points of failures for what it's purpose was for me - simply just developing locally.

So that's why I decided to build a Vagrant LAMP Box. The box is prepackaged and requires provisioning and no configuration. You simply boot it up and it just works. **It's not for every project, but it sure will help you get straight to it with a lot of them**.

> Are you new to Vagrant? If your new to Vagrant, check out our [getting started guide with Vagrant][2] article, our [Vagrant Share article][10], and our article on [Larvel's Vagrant stack Homestead][11]. If you follow the first tutorial, you can just learn the Vagrant commands but use the Scotch Box instead.

![Scotch Box SSH](https://cask.scotch.io/2014/10/scotch-box-ssh.jpg)

## The MIT License (MIT)
Copyright (c) 2014-2015 Nicholas Cerminara, scotch.io, LLC

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[1]: https://github.com/MiniCodeMonkey/Vagrant-LAMP-Stack
[2]: http://scotch.io/tutorials/get-vagrant-up-and-running-in-no-time
[3]: https://www.vagrantup.com/downloads.html
[4]: https://www.virtualbox.org/wiki/Downloads
[5]: http://www.sequelpro.com/
[6]: http://www.navicat.com/
[7]: http://github.com/scotch-io
[8]: http://twitter.com/scotch_io
[9]: https://github.com/smdahlen/vagrant-hostmanager
[10]: http://scotch.io/tutorials/sharing-your-virtual-machine-on-the-web-with-vagrant-share
[11]: http://scotch.io/tutorials/php/getting-started-with-laravel-homestead
[12]: https://www.vagrantup.com/downloads.html
[13]: https://www.virtualbox.org/wiki/Downloads
[14]: http://192.168.33.10/
[15]: https://github.com/smdahlen/vagrant-hostmanager
[16]: http://box.scotch.io
[17]: http://scotch.io/bar-talk/introducing-scotch-box-a-vagrant-lamp-stack-that-just-works
