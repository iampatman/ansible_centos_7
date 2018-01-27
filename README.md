## Preparing the server you want to provision with ansible

Target OS

- Centos7

On your machine:
- Make sure you have ansbile installed

Create user to use with ansible as root

Create user:
> adduser ansible
Set password
> passwd ansible
Add to root group
> usermod -aG wheel ansible


Granted permission to execute sudo with password

	echo 'ansible ALL=(ALL) ALL' | sudo EDITOR='tee -a' visudo

	echo '%wheel ALL=(ALL) ALL' | sudo EDITOR='tee -a' visudo

	echo '%wheel ALL=(ALL) NOPASSWD: ALL' | sudo EDITOR='tee -a' visudo



User name should be ansible

Edit hosts file and set your ip/domain in server section

Test ssh connection:

	ansible -i hosts server -m ping -u ansible

Run ansible script

	ansible-playbook -i hosts -u ansible main.yaml

Write variables and passwords in vars/server.yml
Encrypt server.yml in advance with the following command

	ansible-vault encrypt server.yml

If you write the location of the cryptographic password in
ansible.cfg, you do not have to hit the password each time
(The contents are only the password)

	vault_password_file = ~/Dropbox/ansible/vault_pass

What is in server.yml

	hostname: 'yourhost' ← Linux host name
	domain: 'yourdomain' ← Main domain
	subdomain: 'subdomain.yourdomain' ← sub domain(using blog)
	username: 'ansible' ← User name ansible ssh
	mailroot: 'youremailaddress' ← E-mail address to transfer root's mail
	monitalert: 'youremailaddress' ← Destination of alert mail from monit
	infopassword: '913336a8ecba7764cd81245c2c6b'
	mariadbrootpassword: 'mariadbrootpassword' ← The password of the mariadb root user
	mackerelapikey: 'yourmackerelapikey' ← mackerel's apikey
	dbname: 'yourdbbame' ← DB name used in mariadb
	dbpassword: 'yourdbpassword' ← That password
	docroot: '/home/html' ← Main document route for nginx
	docrootblog: '/home/blog' ← Document root of blog for nginx
	docrootadminer: '/usr/share/webapps/adminer' ← Adminer's document root for nginx

