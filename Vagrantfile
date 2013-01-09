# All Vagrant configuration is done here. The most common configuration
# options are documented and commented below. For a complete reference,
# please see the online documentation at vagrantup.com.

Vagrant::Config.run do |config|
  config.vm.box = "lucid64"
  config.vm.box_url = "http://files.vagrantup.com/lucid64.box"

  config.vm.network :hostonly, "192.168.3.100"

  config.vm.host_name = "vagrant"
  config.vm.share_folder "wwwdata", "/var/www/project", "../", :nfs => true
  #config.vm.share_folder "project", "/var/www/project", "../project"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"

    chef.json = {
      "main" => {
        "hosts" => [
          "127.0.0.1 project.local"
        ],
        #"environment" => [
          #"SOMEKEY=somevar"
        #],
        "apache2" => {
          "vhost" => [{
            "name" => "project",
            "server_name" => "project.local",
            "docroot" => "/var/www/project/web",
            "dirindex" => "app_dev.php",
            "template" => "vhost.conf.erb"
          }]
        },
        "database" => ["project"],
        "dbuser" => [
          {
            "name" => "root",
            "password" => "root",
            "host" => "%",
            "privileges" => [:all]
          },
         {
           "name" => "project",
          "password" => "project",
            "host" => "localhost",
            "database_name" => "project",
            "privileges" => [:all]
          }
        ],
        #"buildscript" => [
          #"python /var/www/project/bin/build.py"
        #],
        #"s3cmd" => {
          #"access_key" => "YOUR_AWS_ACCESS_KEY",
          #"secret_key" => "YOUR_AWS_SECRET_KEY"
        #},
        "mysql" => true,
        #"python" => true,
        "java" => true,
        "nodejs" => true,
        #"mongodb" => true,
        #"redis" => true,
        #"coffeescript" => true,
      },
      "mysql" => {
        "server_root_password" => "root"
      }
    }

    chef.add_recipe("main")
  end
end
