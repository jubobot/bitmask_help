@title = 'Bitmask for GNU/Linux'
@nav_title = 'Linux'

<%= render({:partial => 'common/notice'}, {:type => 'info', :text => '<b>NOTE:</b> Encrypted email support in Bitmask is still experimental.'}) %>

# Introduction

There are two ways to install Bitmask on Linux, as a **package** or as a stand-alone **bundle**.

* **Packages**: run faster, and are better integrated with the desktop environment.
* **Bundles**: do not require root, and can be installed on a portable thumb drive.

To find out which distribution you are running, open a terminal and type in the following:

    cat /etc/issue

# Stand Alone Bundle

The Bitmask stand alone bundle should work on most recent versions of Debian and Ubuntu. You are welcome to try the bundle on other distributions, it sometimes works. Alternately, you can [[build it from source => https://leap.se/en/docs/get-involved/source]].

Our most recent stable release is only available for a 64 bit kernel. 

<table class="table">
<tr><td>
  <%= render({:partial => 'common/download_button'}, {:link => 'https://dl.bitmask.net/client/linux/stable/Bitmask-linux64-latest.tar.gz', :text => 'Download 64 bit'}) %>
</td><td>
  [[Signature file => https://dl.bitmask.net/client/linux/stable/Bitmask-linux64-latest.tar.gz.asc]]
</td></tr>
</table>

Optionally, you can [[authenticate the signature => signature-verification]] using LEAP's archive signing key.

If you want to try an experimental or release candidate versions of Bitmask, you can browse the [[full list of available downloads => https://dl.bitmask.net/client/linux]].

# Ubuntu Packages

### Ubuntu 16.04 LTS (Xenial Xerus)

<%= render({:partial => 'via_packages'}, {:distro => 'xenial'}) %>

### Ubuntu 15.10 (Wily Werewolf)

<%= render({:partial => 'via_packages'}, {:distro => 'wily'}) %>

### Ubuntu 15.04 (Vivid Vervet)

<%= render({:partial => 'via_packages'}, {:distro => 'vivid'}) %>

# Debian Packages

If you are using Wheezy, then you will need to use the bundle method.

### Debian 8 (Oldstable/Jessie)

<%= render({:partial => 'via_packages'}, {:distro => 'jessie', :os => 'debian', :backport => 'true'}) %>

### Debian Stable (Stretch)

<%= render({:partial => 'via_packages'}, {:distro => 'testing', :os => 'debian'}) %>

### Debian Unstable (Sid)

<%= render({:partial => 'via_packages'}, {:distro => 'sid', :os => 'debian'}) %>

# Upgrading

**From stand-alone bundles**: Bitmask should upgrade itself automatically (for versions equal or later than 0.7.0). If you are running a version prior to 0.7.0, you can download the new bundle and copy the "config" folder from the old bundle directory.

**From packages**: If you are running from packages, then you can trigger an update like so:

    apt-get update
    apt-get dist-upgrade

**NOTE:** When upgrading the version of your operating system, you must also follow the directions listed under "When upgrading the OS" above.

# Latest builds
For the more adventurous we make stand alone bundle builds available after each commit or merge. Currently best tested again cdev.bitmask.net, because of ongoing changes of Soledad. 

  <%= render({:partial => 'common/download_button'}, {:link => 'https://0xacab.org/leap/bitmask-dev/builds/artifacts/master/download?job=bitmask_latest_bundle', :text => 'Download latest experimental bundle'}) %>
