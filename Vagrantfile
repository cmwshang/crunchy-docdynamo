Vagrant.configure(2) do |config|
    config.vm.provider :virtualbox do |vb|
        vb.memory = 2048
        vb.cpus = 4
    end

    config.vm.box = "bento/centos-7.3"
    config.vm.box_version = "2.3.4"

    config.vm.provider :virtualbox do |vb|
        vb.name = "crunchy-docdynamo"
    end

    # Provision the VM
    config.vm.provision "shell", inline: <<-SHELL
        echo 'Build Begin' && date

        # Install XML::Checker::Parser via CPAN since CentOS has no package for it
        echo 'Install Utilities' && date
        yum install -y yum cpanminus
        yum groupinstall -y "Development Tools" "Development Libraries"
        cpanm install --force XML::Checker::Parser

        echo 'Install Latex' && date
        yum -y install texlive texlive-*.noarch ghostscript

        echo 'Get DocDynamo' && date
        yum install -y git
        git clone https://github.com/cmwshang/docdynamo.git /docdynamo

        echo 'Get Crunchy Containers' && date
        git clone https://github.com/CrunchyData/crunchy-containers.git /crunchy-containers
        cd /crunchy-containers && git checkout 2aa616a48f58039dcdb78a9be5548d9fa7c05fa9

        echo 'Build End' && date
    SHELL

  # Don't share the default vagrant folder
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Mount project path for testing
  config.vm.synced_folder ".", "/crunchy-docdynamo"
end
