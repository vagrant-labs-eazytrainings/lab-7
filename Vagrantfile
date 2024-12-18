RAM= "2048"
CPU= 2
IP= "10.0.0.10"

Vagrant.configure("2") do |config|
  config.vm.box = "jak-devops/nginx"
  config.vm.box_version = "0"
  config.vm.hostname = "web-server"
  config.vm.network "private_network", ip: IP
  config.vm.synced_folder "static-website-example/", "/usr/share/nginx/html"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = RAM
    vb.cpus = CPU
  end
end
