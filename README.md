Ansible Role for Nextcloud - an Open Source Cloud Storage
=========================================================

This Ansible role can be used to deploy, update and reconfigure Nextcloud.
Nextcloud is a suite of client-server software for creating and using file hosting services. Nextcloud application functionally is similar to Dropbox. Unlike Dropbox, Nextcloud does not offer off-premises file storage hosting.
See also: [Nextcloud Homepage](https://nextcloud.com/)

## Features

- Automatically updates Nextcloud
- Adjustable data folder path
- Adjustable redis settings
- Adjustable memcache settings
- Many config.php settings can be adjusted using ```nextcloud_config_settings```

## Install role via Ansible Galaxy

```
ansible-galaxy install dasleo.ansible_role_gitea
```

## Example Playbook

```yml
---

- hosts: nextcloud_server
  become: yes
  vars:
    nextcloud_version: 14.0.10
    nextcloud_service_user: nextcloud
    nextcloud_path: /var/www/nextcloud
    nextcloud_user: nextcloud
    nextcloud_urls:
      - cloud.example.net
    nextcloud_admin: admin
    nextcloud_db_host: localhost
    nextcloud_db_user: nextcloud
    nextcloud_db_password: "{{ nextcloud_db_user_password }}"
    nextcloud_db_name: Nextcloud
    nextcloud_redis_use: true
    nextcloud_redis_config:
      - name: memcache.locking
        value: '\OC\Memcache\Redis'
      - name: 'redis host'
        value: 127.0.0.1
      - name: 'redis port'
        value: '6379'
      - name: 'redis password'
        value: "{{ nextcloud_redis_password }}"
      - name: 'redis timeout'
        value: '1.5'
    nextcloud_config_settings:
      - name: memcache.local
        value: '\OC\Memcache\APCu'
      - name: updater.release.channel
        value: production
      - name: auth.bruteforce.protection.enabled
        value: 'true'
      - name: mail_smtpmode
        value: smtp
      - name: mail_smtpauthtype
        value: LOGIN
      - name: mail_from_address
        value: cloud
      - name: mail_domain
        value: example.net
      - name: mail_smtphost
        value: mail.example.net
    nextcloud_use_custom_apps: true
    nextcloud_apps:
      - bruteforcesettings
      - twofactor_totp
  roles:
    - { role: dasleo.ansible-role-nextcloud }
```

## Updating Nextcloud

This Ansible role automatically compares the installed version with the version set by ```nextcloud_version``` and upgrades if ```nextcloud_version``` is higher than the currently installed one.

## License

>Copyright 2019-present Philipp Leonhardt
>
>Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
>
>1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
>2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
>3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
>
>THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
