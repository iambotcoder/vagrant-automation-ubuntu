# 🚀 Vagrant Virtual Machine Automation

---

## 📖 Overview
This project automates the creation and configuration of virtual machines using Vagrant with VirtualBox. The setup includes private and public networking, synced folders, and provisioning options to streamline VM deployment.

---

## 📑 Table of Contents
- [Prerequisites](#prerequisites) 🔑
- [Architecture](#architecture) 🗺️
- [Setup & Installation](#setup-and-installation) 🛠️
- [Vagrant Setup](#vagrant-setup) 🐳
- [Cleaning Up Resources](#cleaning-up-resources) 🧹
- [Conclusion](#conclusion) ✅

---

## 🔑 Prerequisites
Before starting, ensure you have the following installed:
- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- A terminal or command prompt with administrative privileges

---

## 🗺️ Architecture
This project utilizes Vagrant to set up an Ubuntu virtual machine with specific configurations:
- **Base OS:** Ubuntu Jammy 64-bit
- **Networking:**
  - Private network with a static IP (`192.168.56.14`)
  - Public network for external access
- **Resource Allocation:**
  - Memory: 1600MB
  - CPUs: 2
- **Synced Folder:**
  - Maps `D:\scripts\shellscripts` on the host to `/opt/scripts` in the VM
- **Provisioning (Optional):**
  - Can be configured to install packages (like Apache) automatically

### Workflow:
1. **Initialize Vagrant** – Create the required configuration.
2. **Start the VM** – Boot the virtual machine.
3. **Access the VM** – SSH into the machine.
4. **Validate Network Settings** – Check assigned IPs.
5. **Destroy the VM** – Cleanup once testing is complete.

---

## 🛠️ Setup & Installation

### 1⃣ Initialize Vagrant:
```bash
vagrant init
```

### 2⃣ Start the Virtual Machine:
```bash
vagrant up
```

### 3⃣ Check VM Status:
```bash
vagrant status
```

### 4⃣ SSH into the VM:
```bash
vagrant ssh
```

### 5⃣ Check Network Configuration:
```bash
ip addr show
``` 

### 6⃣ Exit the VM:
```bash
exit
``` 

## 🐾 Vagrant Setup 🖥️

Below is the `Vagrantfile` configuration used for this project:

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Use the Ubuntu Jammy box
  config.vm.box = "ubuntu/jammy64"

  # Private network for host-only access
  config.vm.network "private_network", ip: "192.168.56.14"

  # Public network for bridged access
  config.vm.network "public_network"

  # Sync a directory from the host to the guest
  config.vm.synced_folder "D:\\scripts\\shellscripts", "/opt/scripts"

  # VirtualBox provider-specific configurations
  config.vm.provider "virtualbox" do |vb|
    # Allocate memory and CPUs
    vb.memory = "1600"
    vb.cpus = "2"
  end

  # Keep the default insecure SSH key
  config.ssh.insert_key = false

  # Provision the VM with essential updates (optional)
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  #   echo "Iambot"
  # SHELL
end
``` 

### 🧹 Cleaning Up Resources

To remove the VM and free up system resources, run the following commands in order:

### 1⃣ Destroy the Virtual Machine:
   ```bash
   vagrant destroy
   ```
### 2⃣ Remove Unused Vagrant Instances:
   ```bash
   vagrant global-status --prune
   ```
---

## ✅ Conclusion

This project demonstrates how to automate VM provisioning using Vagrant and VirtualBox, making it easier to manage development and testing environments efficiently.

---

## 👨‍🏫 Instructor

This project was guided by Imran Teli, who provided valuable mentorship throughout the process.
