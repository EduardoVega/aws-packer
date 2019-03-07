Vagrant.configure("2") do |config|
    config.vm.box = "dummy.box"

    config.vm.synced_folder ".", "/vagrant", disabled: true
  
    config.vm.provider :aws do |aws, override|
      aws.access_key_id = ENV['ACCESS_KEY']
      aws.secret_access_key = ENV['SECRET_KEY']
      aws.keypair_name = "ec2-vms"
      aws.ami = "ami-0c9a4444202e59c0f"
      aws.region = "us-east-1"
      aws.instance_type = "t2.micro"
      aws.security_groups = "sg-0ac866c346dd50e56"
      aws.associate_public_ip = true
      aws.subnet_id = "subnet-098bf0e8d234c4578"
      aws.tags = {
        'Type' => 'Vagrant',
      }
      override.ssh.username = "centos"
      override.ssh.private_key_path = ENV['PRIVATE_KEY']

    end
end