# polipo-box

Example setup for running [polipo](http://www.pps.univ-paris-diderot.fr/~jch/software/polipo/) proxy server in a [Vagrant](http://www.vagrantup.com/) box.

This can be used in combination with the [vagrant-proxyconf][proxyconf] plugin to cache most HTTP traffic of the VMs to speed up Vagrant usage. The configuration should be easy to customize either as well for local machines as for cloud providers.

Polipo does its best also when offline. But as it can't cache HTTPS traffic, you might want to use [vagrant-cachier](https://github.com/fgrehm/vagrant-cachier) in combination with vagrant-proxyconf if you aim to use Vagrant without internet connection at times.

Note that the example configuration allows access from everywhere. That should be fine when running on local machine or internal network, but not a good idea if the machine is accessible from internet.

## Usage

* Install Vagrant 1.2 or later: [www.vagrantup.com/downloads](http://www.vagrantup.com/downloads)

* With Vagrant versions older than 1.7, install the vagrant-omnibus plugin:

        vagrant plugin install vagrant-omnibus

* Clone this repository and customize as needed:

        git clone https://github.com/tmatilai/polipo-box.git
        cd polipo-box
        # edit Vagrantfile

* Spin up the box

        vagrant up

### Configuring vagrant-proxyconf

* Install the vagrant-proxyconf plugin:

        vagrant plugin install vagrant-proxyconf

* Configure all Vagrant boxes to use the proxy by default. Put something like the following to _$HOME/.vagrant.d/Vagrantfile_:
```ruby
Vagrant.configure("2") do |config|
  config.proxy.http     = "http://192.168.33.200:8123/"
  config.proxy.no_proxy = "localhost,127.0.0.1"
  # other global configuration
end
```
* The proxy configuration can be overridden in project specific Vagrantfiles or with environment variables. See the vagrant-proxyconf [documentation][proxyconf] for details.

[proxyconf]: http://tmatilai.github.io/vagrant-proxyconf/
