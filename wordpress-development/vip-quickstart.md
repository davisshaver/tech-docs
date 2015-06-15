# VIP Quickstart

Because Fusion.net is hosted on WordPress.com VIP, we use [VIP Quickstart](https://github.com/Automattic/vip-quickstart) as our WordPress development environment.

## Setting up VIP Quickstart

1. Follow the <a href="https://vip.wordpress.com/documentation/quickstart/">VIP Quickstart</a> documentation to configure the virtual machine. If all goes well, you'll have a working WordPress installation at `vip.dev`.
1. Recursively clone the Fusion theme repo into `/www/wp-content/themes/vip/`. Make sure you keep the folder name as `fusion-theme`. Emphasis on _recursively_; we use git submodules, so the sky will fall on your head if you don't have them checked out. You can use `git clone --recursive <github-url>`
1. <a href="http://vip.local/wp-admin/network/site-new.php">Create a new site</a> on the WordPress network called, ‘Fusion’, and have it live at `vip.local/fusion/`. Because of some idiosyncracies in WordPress, it's better to have your working site as a secondary site on the network.
1. <a href="http://vip.local/wp-admin/network/themes.php">Enable the Fusion theme</a> to be activated on the site..</li>
1. Get sample content. You can use your new access to production to generate an export for the past month or so. You will find it easier to import with WP-CLI than the WordPress import tool, which will likely time out. See below for notes on importing content to VIP Quickstart.
1. Begin developing!

## Updating VIP Quickstart

VIP Quickstart has its own update mechanism. First, make sure the Quickstart code is up to date with `git pull origin master`. Then, inside the Quickstart working directory, you can run `vagrant provision`, which will re-run all provisioning steps.
    
## How to import a post database

1. SCP the zip into your vagrant instance with `scp _file_ vagrant@vip.local:/home/vagrant/`
1. Unzip the file
1. Import the file with `wp import <folder> --authors=create --skip="image_resize" --url=vip.local/fusion`

## What to do if you want fusion-theme somewhere outside VIP Quickstart

Add a line like this to your vagrant configuration file:
```
config.vm.synced_folder "/$PATH_TO/fusion-theme/", "/srv/www/wp-content/themes/vip/fusion-theme"
```

