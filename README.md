# ansible-role-docker-registry
Tested on Ansible 2.4.2 and Ubuntu 16.04  
This role depends on docker and letsencrypt roles.

## Playbook sample
Setup docker registry and web ui optionally.  
registry_web_port (optional) : default is 8080  
s3 (optional) : If this is unset, local disk will be backend storage.  
install_registry_web: If set, registry web will be installed.
```yaml
- hosts: registry
  become: yes
  roles:
    - role: docker-registry
      cert_domain: registry.example.com
      cert_email: admin@example.com
      cert: '/etc/letsencrypt/live/{{ cert_domain }}/fullchain.pem'
      key: '/etc/letsencrypt/live/{{ cert_domain }}/privkey.pem'
      cert_issuer: example_issuer
      registry_web_port: 7070
      s3:
        bucket: S3_BUCKET_NAME
        access_key: S3_ACCESS_KEY
        secret_key: S3_SECRET_KEY
        region: S3_REGION
      install_registry_web: true
```
