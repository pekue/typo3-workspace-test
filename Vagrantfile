# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = 'precise64'

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  # Assign this VM to a host-only network IP, allowing you to access it
  # via the IP. Host-only networks can talk to the host machine as well as
  # any other machines on the same network, but cannot be accessed (through this
  # network interface) by any external networks.
  config.vm.network :hostonly, '192.168.156.40'

  # Assign this VM to a bridged network, allowing you to connect directly to a
  # network using the host's network device. This makes the VM appear as another
  # physical device on your network.
  # config.vm.network :bridged

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  # config.vm.forward_port 80, 8080

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  config.vm.share_folder 'htdocs-folder', '/var/www/workspace_test_environment/htdocs', 'htdocs', :group => 'www-data', :extra => 'dmode=770,fmode=660'

  config.vm.provision :chef_solo do |chef|
    # We're going to download our cookbooks from the web
    chef.cookbooks_path = 'config/vm/cookbooks'

    # Tell chef what recipe to run. In this case, the `vagrant_main` recipe
    # does all the magic.
    chef.add_recipe('apt')
    chef.add_recipe('apache2')
    chef.add_recipe('apache2::mod_php5')
    chef.add_recipe('php')
    chef.add_recipe('php::module_mysql')
    chef.add_recipe('php::module_curl')
    chef.add_recipe('php::module_gd')
    chef.add_recipe('mysql')
    chef.add_recipe('mysql::server')
    chef.add_recipe('vagrant_main')

    chef.json = {
      'mysql' => {
        'server_root_password' => 'iloverandompasswordsbutthiswilldo',
        'server_repl_password' => 'iloverandompasswordsbutthiswilldo',
        'server_debian_password' => 'iloverandompasswordsbutthiswilldo',
        'bind_address' => '127.0.0.1'
      },
      'php' => {
        'conf_dir' => '/etc/php5/apache2'
      }
    }
  end
end