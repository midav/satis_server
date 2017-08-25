Vagrant.configure("2") do |config|

  vms = [
    { :name => "centos", :box => "centos/7" },
  ]

   config.vm.network "private_network", ip: "192.168.33.10"

  vms.each do |opts|
    config.vm.define opts[:name] do |m|
      m.vm.box = opts[:box]
      m.vm.provider "virtualbox" do |v|
        v.cpus = 1
        v.memory = 256
      end
       m.vm.provision "ansible" do |ansible|
         ansible.playbook = "tests/test.yml"
         ansible.verbose = 'vv'
         ansible.sudo = true
       end
    end
  end
end