Ansible Role for Nextcloud - an Open Source Cloud Storage
=========================================================

## Example Playbook

```
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
