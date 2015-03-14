ansible-role-ssl-certs
======================

Generate and/or deploy SSL certificate

Available on Ansible galaxy : https://galaxy.ansible.com/list#/roles/3115

# Examples
## Example to generate a SSL certificate (self-signed)
```
 - hosts: all
   roles: 
     - jdauphant.ssl-certs
```
This will create in
- /etc/ssl/myserver.mydomain.com.key 
- /etc/ssl/myserver.mydomain.com.pem


## Example to deploy a SSL certificate
```
 - hosts: all
   roles: 
    - role: jdauphant.ssl-certs
      ssl_certs_common_name: "example.com"
```
The certificat have to be place in ssl/example.com.key and ssl/example.com.pem .
If they don't exist they will be generated (self-signed) as /etc/ssl/example.com.key  and /etc/ssl/example.com.com.key 


## Example 2 to deploy a SSL certificate by specified the local key/pem files path
```
 - hosts: all
   roles: 
    - role: jdauphant.ssl-certs
      ssl_certs_local_privkey_path: 'files/key/example.com.key'
      ssl_certs_local_cert_path: 'files/pem/example.com.pem'
```

## Example to use this role with my Nginx role ( https://github.com/jdauphant/ansible-role-nginx )
```
 - hosts: all
   roles: 
     - jdauphant.ssl-certs
     - role: jdauphant.nginx
       nginx_configs: 
          ssl:
               - ssl_certificate_key {{ssl_certs_privkey_path}}
               - ssl_certificate     {{ssl_certs_cert_path}}
       nginx_sites:
          default:
               - listen 443 ssl
               - server_name _
               - root "/usr/share/nginx/html"
               - index index.html
```
