# -*- mode: ruby -*-
# vi: set ft=ruby :

#setting environmental variable for DATABASE_URL
env_var_cmd = ""
if ENV['DATABASE_URL']
  value = ENV['DATABASE_URL']
  env_var_cmd = <<CMD
echo "export DATABASE_URL=#{value}" | tee -a /home/vagrant/.profile
CMD
end

script = <<SCRIPT
#{env_var_cmd}
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.network 'forwarded_port', guest: 9292, host: 9292
  # guestbook VM
  config.vm.define "v1", primary: true do |v1|
  config.vm.provision :shell, :inline => script
    v1.vm.box = "ubuntu/trusty64"
    v1.vm.provision "ansible" do |ansible|
      ansible.playbook = 'provisioning/dev.yml'
      ansible.verbose = 'vvv'
    end
  end
  # Use vagrant-cachier to cache apt-get, gems and other stuff across machines
  # Also consider using vagrant-exec, vagrant-faster and vagrant-omnibus
  if Vagrant.has_plugin?('vagrant-cachier')
    config.cache.scope = :box
  else
    puts "Run `vagrant plugin install vagrant-cachier` to reduce caffeine intake when provisioning"
  end

end
