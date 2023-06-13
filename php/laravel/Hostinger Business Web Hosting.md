# Hostinger Business Web Hosting

Created: 13-06-2023
Last Updated: 13-06-2023

> **_Local Laravel Project is Ready to Deploy_**

## Get SSH Access

**Home** > **Business Web Hosting** > **Manage** > **Advanced** > **SSH Access**

## Activate SSH

By clicking `Enable` button in SSH Status tab.

## PHP configuration

Set PHP version to PHP 8.2

## Composer Updation Issue

> Issue: Permission Denied

### Solution:

Hostinger comes with `composer` and `composer2` on shared hosting with, and by default all the projects are set to use composer i.e., `composer 1.1.0`, what you could do is either modify the files under `/usr/local/bin` which most probably is not going to be possible due to the fact that this directory is not writable, so here's the solution:

`SSH` into your shared hosting using your preferred `ssh` client.
Make sure you are in your `home` directory `cd ~`
Edit your shell configurations file `nano .bashrc` (for `Bash`) or `nano .zshrc` (for `Zsh`)
Add the following line to the end of the file: `alias composer="php /usr/local/bin/composer2.phar"` (This will use `composer 2.5.5` at the time of writing this answer)
Save the file by pressing `CTRL+X`, then `Y`, then `ENTER`
Reload your shell configuration by running the command `source ~/.bashrc` or `source ~/.zshrc`, depending on which shell you're using.
This should be it, now running `composer --version` will give you Composer version `2.5.5` instead of `1.1.0`

Note: be advised that this will apply composer at global level, affecting all of your projects using composer under the same hosting, proceed with caution.
