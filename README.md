# Pi-hole Ansible Role

Automate the installation and configuration of Pi-hole using Ansible. This role sets up Pi-hole in unattended mode, configures system users/groups, and prepares the required configuration files for a smooth deployment.

---

## 🚀 Features

- Automated, unattended Pi-hole installation
- Pre-configures Pi-hole using a templated `pihole.toml`
- Ensures required system users and groups exist
- Handles necessary directory creation and permissions
- Downloads and runs the official Pi-hole installer script
- Easily customizable via Ansible variables and templates

---

## 📦 Requirements

- Ansible installed on your control machine (`sudo apt install ansible`)
- SSH access to the target host(s)
- Supported OS: Debian, Ubuntu, Raspberry Pi OS

---

## 🗂️ Role Structure

```
roles/
└── pihole/
    ├── tasks/
    │   └── main.yml
    └── templates/
        └── pihole.toml.j2
```

---

## ⚙️ Variables

You can customize Pi-hole settings by editing `pihole.toml.j2` in the `templates` directory.  
Common variables include:

- `FTLCONF_webserver_api_password`: Web dashboard password
- `FTLinterface`: Network interface Pi-hole listens on
- `REPLY_ADDR4`: IPv4 address for Pi-hole
- DNS upstreams, blocking mode, logging options, etc.

---

## 📝 How It Works

1. **Detects the primary network interface and IPv4 address**  
   Uses Ansible facts to set `pihole_interface` and `pihole_ipv4`.

2. **Installs required dependencies**  
   Ensures `curl` and `sudo` are present.

3. **Creates system user and group for Pi-hole**  
   Adds a `pihole` user and group for security.

4. **Prepares configuration directory and file**  
   Creates `/etc/pihole` and renders `pihole.toml` from the Jinja2 template.

5. **Downloads the official Pi-hole installer script**  
   Fetches the latest install script from Pi-hole.

6. **Runs the installer in unattended mode**  
   Installs Pi-hole using the pre-configured settings.

---

## 🔧 Usage

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/pihole-ansible.git
cd pihole-ansible
```

### 2. Update your inventory

Edit the `inventory` file to list your Pi-hole host(s):

```ini
[pihole]
192.168.1.100 ansible_user=pi
```

### 3. Customize configuration (optional)

Edit `roles/pihole/templates/pihole.toml.j2` to set your desired Pi-hole options.

### 4. Run the playbook

```bash
ansible-playbook -i inventory/hosts playbook.yml
```

---

## 🌐 Accessing Pi-hole

After installation, access the Pi-hole web dashboard at:

```
http://<your_pi-hole_ip>/admin
```

- **Username:** admin
- **Password:** As set in `pihole.toml.j2` (`FTLCONF_webserver_api_password`), default is usually `testpass123` unless changed.

---

## 🛡️ Security & Maintenance

- Pi-hole manages its own log rotation.
- For best security, change the default web password after installation.
- Keep your system updated for latest security patches.

---

## 🤝 Contributing

Feel free to open issues or submit pull requests to improve this role!

---

## 📄 License

MIT License. See [LICENSE](LICENSE) for details.