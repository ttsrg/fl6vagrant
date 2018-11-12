Vagrant.configure("2") do |config|
 config.vm.define "ttserg" do |config|
  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = '~/.ssh/id_rsa'
    override.vm.box = 'digital_ocean'
    override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
    override.nfs.functional = false
    config.env.enable
    provider.token = ENV['MY_TOKEN']
#    provider.token = ENV['ov_token']
    provider.image = 'ubuntu-16-04-x64'
    provider.region = 'nyc1'
    provider.size = '512mb'
 
# config.vm.synced_folder "." "/vagrant", disabled: true
  end
 end

   config.vm.provision "shell", inline: <<-SHELL
      apt update > /dev/null
      test -x /usr/bin/python || apt-get -y install python2.7-minimal
      update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
   SHELL

  # Run Ansible from the Vagrant Host
  #
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "ansible/app.yml"
  end

end
