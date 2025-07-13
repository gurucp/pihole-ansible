# 🚀 Pi-hole Adlists Automation with Ansible

This project automates managing Pi-hole adlists (blocklists) using Ansible and `sqlite3`. It allows you to keep your blocklists organized in a separate YAML file and deploy them easily to your Pi-hole server.

---

## 🗂️ Project Structure

vars # Variable 
inventory # Ansible inventory file with Pi-hole host information

manage_pihole_adlists.yml # Main Ansible playbook to manage adlists

adlists.yml # YAML file containing your blocklists

README.md # This instructions file


---

## 💡 Features

✅ Manage large lists of blocklists easily  
✅ Store blocklists in a separate YAML file for better organization  
✅ Automatically install required dependencies (e.g., sqlite3)  
✅ Automatically update Pi-hole gravity after changes  
✅ Clean and reusable structure, ready for Git

---

## ⚙️ Requirements

- Ansible installed on your local machine (e.g., `sudo apt install ansible`)
- SSH access to your Pi-hole host
- Pi-hole server (tested on Raspberry Pi OS and Ubuntu)

---

## 🛠️ Setup Instructions

### 1️⃣ Clone this repository


git clone https://github.com/YOUR_GITHUB_USERNAME/pihole-ansible.git
cd pihole-ansible


2️⃣ Update the inventory file
Edit the inventory file to include your Pi-hole server's IP address and SSH user.

Example:
[pihole]
192.168.0.2 ansible_user=pi


## Very Important:!!!!
Edit vars.yml file 
cleanup_adlists: true # If it is set to true it will remove all existing on your pihole and add new entries 
cleanup_adlists: false # If it is set to false, it will not remove existing once rather it will add whatever in the addlists.yml


3️⃣ Edit adlists.yml
Add or remove blocklists as needed inside adlists.yml.

Example snippet:
adlists:
  - "https://adaway.org/hosts.txt"
  - "https://v.firebog.net/hosts/AdguardDNS.txt"
  # Add more as needed


4️⃣ Run the playbook

ansible-playbook -i inventory manage_pihole_adlists.yml

💥 What it does
Ensures sqlite3 is installed on your Pi-hole host

Optionally removes existing adlists (if cleanup step enabled)

Inserts all blocklists from adlists.yml into Pi-hole's database

Updates Pi-hole gravity to apply new lists

Prints current adlists for verification


Optional: Cleanup existing adlists
If you want to reset and remove all existing adlists before adding new ones, make sure the cleanup task is enabled in manage_pihole_adlists.yml.

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



