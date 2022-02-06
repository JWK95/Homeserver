# HomeServerAutomation
An ansible playbook to deploy and configure my home server.

This playbook assumes a fresh Raspbian 64-bit install, access to a non-root user with sudo privileges and a public SSH key.

## Hardware
For my server I use a Raspberry Pi 4 Model B with 8GBs of RAM with an attached Geekworm X735 Expansion board and a GeeekPi X825 SATA Expansion board for 1TB of SSD storage.

## Software
My server currently runs Raspbian 64-bit, however this playbook should be compatible with any Debian based OS

### Services
- [Jellyfin](https://jellyfin.org/) - Media Server
- [Pi-hole](https://pi-hole.net/) - DNS level ad blocker
- [Homer](https://github.com/bastienwirtz/homer) - Interactive web dashboard

### Other
- [x735 Safe shutdown script](https://github.com/thorkseng/x735-v2.5)
- [Samba](https://www.samba.org/samba/)

## Prerequisites
Before starting ensure you have access to a non-root sudo user and have added your public SSH key to the server.
If you haven't done this yet, see below:

Generate SSH Key:
```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/homeserver -C "your_email@example.com"
```

Add SSH Key to the server:
```
ssh-copy-id -i ~/.ssh/homeserver username@server
```

## Usage
Install Ansible (Debian):
```
sudo apt install ansible
```

Clone the repository:
```
git clone https://github.com/JoeC7756/HomeServerAutomation.git
```

Create and update hosts file using the provided template:
```
cp examplehosts hosts
vim hosts
```

Create a host variable file and adjust the values:
```
mkdir -p host_vars/HOSTNAME
vim host_vars/HOSTNAME/vars.yml
```

Install the dependencies:
```
ansible-galaxy install -r requirements.yml
```

Run the playbook:
```
ansible-playbook run.yml -K (First time)
ansible-playbook run.yml (Subsequent runs)
```