# Apache-saml-sp role

This is the ansible apache-saml-sp role. It can be used to set up the plugin mod_auth_mellon on an Apache2 server.  
This plugin allows you use to connect your application to a SAML2 Identity Provider. 

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
git clone https://github.com/Wardaar/apache-saml-sp.git
cd ..
mv roles/apache-saml-sp/playbook.yaml .
```

## SSL Certificate

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

## Run playbook

```
ansible-playbook playbook.yaml
```

## Service provider metadata

Send SP metadata to your Identity Provider to register as a Service Provider
```
/etc/apache2/mellon/mellon_metadata.xml
```

## Configuration: Role Variables

```
nano playbook.yaml
```

* `app_fqdn`, the fqdn of your application, defaults to app.changeme.com.
* `idp_metadata`, path to the extracted metadata of your Identity Provider.
* `cert_path`, path to the application SSL certificate.
* `key_path`, path to the application SSL key.

## Playbook Example

```
- name: Install SAML SP
  hosts: localhost
  become: yes
  roles:
    - role: apache-saml-sp
  vars:
    - app_fqdn: "app.example.com" # app.cr14
    - idp_metadata: "/home/user/idp_metadata.xml" #path to IDP metadata
    - cert_path: "/home/user/app.crt" #path to SSL certificate
    - key_path: "/home/user/app.key" #path to SSL key

```

## License 

MIT

## Author Information

Benjamin GUILLOUZO
Tanguy PASCALE
Benjamin REICHLING
Valentin THIRION
