### Please note
Using `bootstrap` tag will install:
 - php7.1, 
 - php-fpm, 
 - Nginx, 
 - Composer, 
 - newest Symfony version.

If you additionally need **Mysql** please use `mysql` tag. It will install Percona Server 5.7.

**Another thing**: `mysql_secure_installation.yml` task with tag `mysql_secure` at the moment is not finished.

---

### Playbook

**File:** playbook.yml

```
---
 
- hosts: "my-all"
  serial: 1
  
  vars_files:
    - "roles/{{ role_path | basename }}/vars/{{ env }}.yml"

  roles:
     - { role: ansible-role-p7-symfony }
```


### Inventory
**File:** inventory
```
[development]
server(s)-address(es)

[production]


[my-all:children]
development
production

[development:vars]
env=development

[production:vars]
env=production

```


### Deploy
```
ansible-playbook playbook.yml -i inventory --limit "development" --tags bootstrap
```

### Tags
* bootstrap
* composer
* firewalld
* nginx
* other-packages
* php-packages
* php-changes
* php-fpm
* symfony
* mysql
* mysql_secure

---

**Works on:** 
  - Centos 7