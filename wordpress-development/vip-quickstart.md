# VIP Quickstart

Because Fusion.net is hosted on WordPress.com VIP, we use [VIP Quickstart](https://github.com/Automattic/vip-quickstart) as our WordPress development environment.

## Setting up VIP Quickstart

1. Follow the <a href="https://vip.wordpress.com/documentation/quickstart/">VIP Quickstart</a> documentation to configure the virtual machine. If all goes well, you'll have a working WordPress installation at `vip.dev`. Be sure to go through this process *before* cloning or syncing the Fusion theme directory (see below). If the Fusion theme is present, the provisioning process will take forever because it will try to `chmod` and `chown` each file in the theme, including everything in `/node_modules/` and `.git` directories (that's a lot of files).
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

Don't add this until *after* the provisioning step of setting up VIP Quickstart. If you have to reprovision, you'll probably want to remove it beforehand. See the note about how Fusion theme files affect provisioning time in step 1 of Setting up VIP Quickstart for details.

## Using SSL in local development

It takes a bit more manual work, but it is possible to setup your local development environment to use SSL, which is necessary for testing and development of certain areas of the theme. Follow <a href="https://switchcaseblog.wordpress.com/2016/02/22/creating-a-self-signed-ssl-for-local-development-with-vagrant-nginx/">these instructions</a> to get started.

Once you have completed the instructions, you'll need to manually accept the self-signed certificate for the site within your browser(s), instructions vary by browser but Chrome on OS X users can <a href="http://www.robpeck.com/2010/10/google-chrome-mac-os-x-and-self-signed-ssl-certificates/">follow these</a>.
