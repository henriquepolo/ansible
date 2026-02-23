🚀 Ansible Automation Project

This repository contains a modular structure of Ansible playbooks to manage and configure machines on a network in an organized and efficient way.

🌐 Ansible Setup

Ansible is installed on my local machine 💻, which acts as the controller. From this machine, I send commands and execute playbooks on all the hosts in the network remotely.

✅ There’s no need to install Ansible on the other machines.

📡 All commands are sent via SSH to the hosts defined in the inventory (hosts) file.

⚙️ Allows managing multiple machines in a centralized, fast, and efficient manner.

📂 hosts File

The hosts file organizes machines into separate groups, making management with Ansible easier.

💻 Machine Groups

[xubuntu]
Contains the IPs of the Xubuntu machines:

192.168.122.2
192.168.122.144
192.168.122.19
192.168.122.87

[debian]
Contains the IPs of the Debian machines:

192.168.122.36
192.168.122.43
⚙️ Group Variables

[xubuntu:vars] → connection user: ansible_user=devops

[debian:vars] → connection user: ansible_user=debian

✅ Why This Separation Matters

Run tasks only on specific groups 🎯

Define different variables per machine type ⚙️

Keep the inventory organized and easy to maintain 📑

📝 master.yml File

The master.yml file is the central execution point, importing all individual playbooks to ensure all configurations are applied modularly.

📌 Contents of master.yml
- import_playbook: users.yml
- import_playbook: folders.yml
- import_playbook: docker.yml
- import_playbook: basico.yml
- import_playbook: fileserversetup.yml
🚀 How It Works

Each playbook contains specific tasks:

users.yml → user creation 👤

folders.yml → folder setup 📁

docker.yml → Docker installation and configuration 🐳

basico.yml → basic system adjustments ⚙️

fileserversetup.yml → file server setup 📂

The master.yml imports all playbooks in the defined order, ensuring complete execution ✅

Easy maintenance: new playbooks can be added without changing the main file ➕

🔧 How to Use
1️⃣ Execute on All Machines

To apply the playbooks to all hosts in the network:

ansible-playbook -i hosts master.yml --ask-pass --ask-become-pass -vvv
🔹 Parameter Explanation

-i hosts → inventory file with all groups and IPs 💻

master.yml → main file importing all playbooks 📂

--ask-pass → prompts for SSH password 🔑

--ask-become-pass → prompts for sudo password 🛡️

-vvv → enables verbose mode, showing all steps 📝

💡 This command ensures that all hosts defined in the inventory receive the configurations centrally and automatically.

2️⃣ Execute Only on a Specific Group

To apply the playbooks only on Debian machines:

ansible-playbook -i hosts master.yml --limit debian --ask-pass --ask-become-pass -vvv
🔹 Additional Parameter Explanation

--limit debian → restricts execution to the debian group only 🎯

💡 Useful for testing or applying changes to a specific group without affecting other machines.

✅ With this structure, the project allows managing multiple machines in a modular, organized, and secure way, using only your local machine as the Ansible controller.