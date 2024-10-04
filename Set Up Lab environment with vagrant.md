Guide: Setting Up a Windows 11 Environment with Vagrant

1. Install Vagrant and VirtualBox (or Hyper-V)

For VirtualBox:
   1. Download and Install VirtualBox from [VirtualBox Downloads Page](https://www.virtualbox.org/wiki/Downloads).
   2. Install Vagrant from the [Vagrant Downloads Page](https://www.vagrantup.com/downloads).
      ![image](https://github.com/user-attachments/assets/6f469b23-cb5e-4106-b1af-7b8690212579)

   4. Open PowerShell and run:  
      ```bash
      vagrant --version
      vboxmanage --version
      ```

- For Hyper-V:
   1. Open Control Panel and go to **Programs > Turn Windows Features on or off**.
   2. Check **Hyper-V** and click **OK**.
   3. Install Vagrant from the [Vagrant Downloads Page](https://www.vagrantup.com/downloads).
   4. Open PowerShell and run:  
      ```bash
      vagrant --version
      ```


2. Manually Download the Windows 11 Vagrant Box

- For VirtualBox Users:  
  [Download VirtualBox Box]([(https://api.hashicorp.cloud/vagrant/2022-08-01/gusztavvargadr/boxes/windows-11-23h2-enterprise/versions/2302.0.2409/providers/virtualbox/amd64/vagrant.box)])

- For Hyper-V Users:  
  [Download Hyper-V Box]([https://api.hashicorp.cloud/vagrant/2022-08-01/gusztavvargadr/boxes/windows-11-23h2-enterprise/versions/2302.0.2409/providers/hyperv/amd64/vagrant.box)])


3. Set Up the Vagrant Environment

1. Create a new directory:

   ```bash
   mkdir vagrant-lab
   cd vagrant-lab
   ```

2. Add the Windows 11 box:

   ```bash
   vagrant box add windows11 C:/path/to/windows11.box
   ```
C:/path/to/windows11.box should reflect the path the vagrant windows 11 box you downloaded


3. Initialize the Vagrant environment:

   ```bash
   vagrant init windows11
   ```



4. Customize the Vagrantfile for Windows 11
Go into the directory vagrant-lab, open the Vagrantfile file with VScode or notepad, replace the content with the code below:

For VirtualBox Users:

   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "windows11"
     config.vm.network "private_network", ip: "192.168.56.11"
     config.vm.provider "virtualbox" do |vb|
       vb.memory = "4096"
       vb.cpus = 2
       vb.gui = true
       vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
       vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
     end
   end
   ```

For Hyper-V Users:

   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "windows11"
     config.vm.network "private_network", ip: "192.168.56.11"
     config.vm.provider "hyperv" do |hv|
       hv.memory = "4096"
       hv.cpus = 2
       hv.enable_virtualization_extensions = true
     end
   end
   ```

---



5. Spin Up the VM:

   ```bash
   vagrant up
   ```

6. Access the VM** using VirtualBox or Hyper-V Manager.

