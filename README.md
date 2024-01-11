# Ansible LemonLDAP::NG role

This is the ansible mellon role. It can be used to set up the plugin mod_auth_mellon on a server.  
This plugin allows you use an Identity Provider to connect to your application. 

## Installation

Installation of ansible

```
sudo apt install ansible 
``` 

Creation of ansible role repository

```
cd /home/[user]
mkdir .ansible
mkdir .ansible/roles
```

Get ansible profile

```
cd .ansible/roles
git clone https://github.com/Wardaar/apache-mellon-sp
cd ..
mv roles/apache-saml-sp/playbook.yaml .
nano playbook.yaml
```

Generate a self-signed SSL certificate if you don't have one from a provider

```
nano app.cnf
```
Add following directives
```
[req]
default_bits       = 2048
default_keyfile    = private.key
distinguished_name = req_distinguished_name
prompt             = no
[req_distinguished_name]
commonName         = 'fqdn'
```
Execute the following command	
```
sudo openssl req -utf8 -batch -config "app.cnf" -new -x509 -days 3652 -nodes -out "app.crt" -keyout "app.key"
```

Run playbook

```
ansible-playbook playbook.yaml
```

## Configuration: Role Variables

* `app_fqdn`, the fqdn of your application, defaults to app.changeme.com.
* `idp_metadata`, path to the extracted metadata of your Identity Provider.
* `cert_path`, path to the application SSL certificate.
* `key_path`, path to the application SSL key

## Playbook Example

## License 

MIT

## Author Information

Benjamin GUILLOUZO
Tanguy PASCALE
Benjamin REICHLING
Valentin THIRION
