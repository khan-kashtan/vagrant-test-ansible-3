
Vagrant.configure("2") do |config|
  
  config.vm.box_check_update = false
  config.vm.provider :virtualbox do |v|
    v.memory = 512
  end

  config.vm.define "dbserver" do |db|
    db.vm.box = "ubuntu/focal64"
    db.vm.hostname = "dbserver"
    db.vm.network :private_network, ip: "10.10.10.10"
    db.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/site.yaml"
      ansible.inventory_path = "/etc/ansible/hosts/"
      ansible.groups = {
      "db" => ["dbserver"],
      "db:vars" => {"mongo_bind_ip" => "0.0.0.0"}
      }
    end
  end

  config.vm.define "appserver" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.hostname = "appserver"
    app.vm.network :private_network, ip: "10.10.10.20"
    app.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/site.yaml"
      ansible.groups = {
        "app" => ["appserver"],
        "app:vars" => {
          "db_host" => "10.10.10.10"
        }
      }
      ansible.extra_vars = {
        "deploy_user" => "ubuntu"
      }
    end
  end
end