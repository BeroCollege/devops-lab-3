Vagrant.configure("2") do |config|
  # Use Debian Bookworm 64-bit as the base box
  config.vm.box = "debian/bookworm64"

  # Forward port 5000 from the VM to the host (change 8080 to another port if needed)
  config.vm.network "forwarded_port", guest: 5000, host: 8080

  # Provision the VM
  config.vm.provision "file", source: "hello.py", destination: "/home/vagrant/hello.py"

  # Shell provisioner to install dependencies and start the Flask app
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update -y
    sudo apt install -y git nano vim python-is-python3 python3-venv python3-pip

    # Create a virtual environment and activate it
    python3 -m venv /home/vagrant/flask_venv
    source /home/vagrant/flask_venv/bin/activate

    # Install Flask
    pip install Flask

    # Run the Flask app in the background
    nohup flask --app /home/vagrant/hello run --host=0.0.0.0 &
  SHELL
end
