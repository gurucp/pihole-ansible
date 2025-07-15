# 🚀 Pi-hole Install and configure Automation with Ansible

This project automates Installing and configuring using Ansible. 

What does this playbook handle?
- Installs Pi-hole
- Adds blacklists (URLs are listed in `adlists.yml`)
- Installs nftables and configures rules to keep the Pi-hole box safe and secure
- Optimizes performance by configuring Unbound DNS and various kernel parameters
- If you already have adlists configured, you can choose to remove all existing ones and recreate the list

---

## 🗂️ Project Structure

- `vars.yml` — Variable definitions
- `inventory` — Ansible inventory file with Pi-hole host information
- `manage_pihole_adlists.yml` — Playbook to manage Pi-hole adlists
- `adlists.yml` — YAML file containing blocklists
- `README.md` — Project instructions
- `configure_nftables.yml` — Playbook to configure nftables firewall rules
- `install_pihole.yml` — Playbook to install Pi-hole
- `configure_pihole.yml` — Playbook to configure Pi-hole with blocklists
- `optimize_pihole.yml` — Playbook to optimize


---

## 💡 Features

- Automated Pi-hole installation and configuration
- Efficient management of large blocklists
- Blocklists stored in a dedicated YAML file (`adlists.yml`)
- Option to clean up and recreate adlists from scratch
- Automatic installation of required dependencies (e.g., sqlite3)
- Enhanced security with nftables firewall rules
- Optimized DNS performance using Unbound and kernel tweaks
- Automatic updates to Pi-hole gravity after changes
- Modular design for easy recovery from SD card corruption

---

## ⚙️ Requirements

- Ansible installed on your local machine (e.g., `sudo apt install ansible`)
- SSH access to your Pi-hole host
- Pi-hole server (tested on Raspberry Pi OS and Ubuntu), Ubuntu 24/22 VM

---

## 🛠️ Setup Instructions

### 1️⃣ Clone this repository

```bash
git clone https://github.com/gurucp/pihole-ansible.git
cd pihole-ansible
```

2️⃣ Update the inventory file
Edit the inventory file to include your Pi-hole server's IP address and SSH user.

Example:
```bash
[pihole]
192.168.0.2 ansible_user=pi
```

## Very Important:!!!!
```bash
Edit vars.yml file 
cleanup_adlists: true # If it is set to true it will remove all existing on your pihole and add new entries 
cleanup_adlists: false # If it is set to false, it will not remove existing once rather it will add whatever in the addlists.yml
```

3️⃣ Edit adlists.yml
Add or remove blocklists as needed inside adlists.yml.

Example snippet:
```bash
adlists:
  - "https://adaway.org/hosts.txt"
  - "https://v.firebog.net/hosts/AdguardDNS.txt"
  # Add more as needed
```
Update the vars.yml file 

pihole_web_password: "testpass123" # Set password here 
pihole_blocklists_cleanup: true    # Set to true if you are reconfiguring the pihole and would like to       remove existing addlist 


4️⃣ Run the playbook
```bash
ansible-playbook -i inventory manage_pihole_adlists.yml
```

❤️ Credits
Inspired by community-maintained blocklists, including:

Hagezi

Firebog

AdGuard

Perflyst

and many more


License
This project is licensed under the MIT License. See LICENSE for details.


⭐ Contributing
Feel free to open issues or pull requests to improve or update blocklists and tasks.



