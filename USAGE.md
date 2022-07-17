# Usage

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
git clone https://github.com/JoeC7756/Homeserver.git
```

Create and update hosts file using the provided template:
```
cp examplehosts hosts
vim hosts
```

Create a host variable file and adjust the default values:
```
mkdir -p host_vars/HOSTNAME
vim host_vars/HOSTNAME/main.yml
```

Some notable values to change are: 
```
pihole_webpassword: "SuperSecurePiHolePassword"
samba_password: "SuperSecureSambaPassword"
certs_email: "YOUR_EMAIL_ADDRESS"
cloudflare_api_token: "YOUR_CLOUDFLARE_TOKEN"
domain: "YOUR_DOMAIN"
```

Install the dependencies:
```
ansible-galaxy install -r requirements.yml
```

Run the playbook:
```
ansible-playbook main.yml -K (First time)
ansible-playbook main.yml (Subsequent runs)
```
