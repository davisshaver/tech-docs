# VIP Quickstart

Because Fusion.net is hosted on WordPress.com VIP, we use [VIP Quickstart](https://github.com/Automattic/vip-quickstart) as our WordPress development environment.

## Setting up VIP Quickstart

1. Follow the <a href="https://vip.wordpress.com/documentation/quickstart/">VIP Quickstart</a> documentation. You should now have a running WordPress installation
1. Recursively clone the Fusion theme repo into `/www/wp-content/themes/vip/`. Make sure you keep the folder name as `fusion-theme`. Emphasis on _recursively_; we use git submodules, so the sky will fall on your head if you don't have them checked out. You can use `git clone --recursive <github-url>`
1. <a href="http://vip.local/wp-admin/network/site-new.php">Create a new site</a> on the WordPress network called, ‘Fusion’, and have it live at `vip.local/fusion/`.
1. <a href="http://vip.local/wp-admin/network/themes.php">Enable the Fusion theme</a>.</li>
1. Get sample content. <a href="https://www.dropbox.com/sh/82rgc3gjq4w7egq/AACSBn5Cl-2xkeq6hd9cfvpIa?dl=0">Here’s all shows/videos + March 2015 posts.</a> You will find it easier to import with WP-CLI than the WordPress import tool, which will likely time out. See below for notes on importing content to VIP Quickstart.
1. Begin developing!

## Updating VIP Quickstart

Go to the VIP Quickstart folder and run the following commands.

    vagrant ssh
    cd /srv/www/wp; svn up
    
    
## How to import a post database

1. SCP the zip into your vagrant instance with <code>scp _file_ vagrant@vip.local:/home/vagrant/</code>
1. Unzip the file
1. Import the file with <code>wp import _folder_ --authors=create --skip="image_resize" --url=_url of your instance_</code>

## What to do if you want fusion-theme somewhere outside VIP Quickstart

Add a line like this to your vagrant configuration file:
```
config.vm.synced_folder "/$PATH_TO/fusion-theme/", "/srv/www/wp-content/themes/vip/fusion-theme"
```

