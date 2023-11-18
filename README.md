# PGBack Ansible Role

Ansible role for backup PostgreSQL database into Amazon S3 using a Linux cron job.

## Installation

```yml
# requirements.yaml
- src: git@github.com:RashadAnsari/ansible-role-pgback.git
  scm: git
  version: master
  name: pgback
```

## Role Variables

``` yaml
postgresql_port: 5432
postgresql_host: "localhost"
postgresql_user: "postgres"
postgresql_database: "postgres"
postgresql_password: "{{ lookup('env', 'POSTGRES_PASSWORD') }}"

s3_use_https: true
s3_bucket_name: pg-backups
s3_region: "{{ lookup('env', 'AWS_REGION') }}"
s3_host_base: "https://s3.{{ s3_region }}.amazonaws.com"
s3_access_key: "{{ lookup('env', 'AWS_ACCESS_KEY_ID') }}"
s3_secret_key: "{{ lookup('env', 'AWS_SECRET_ACCESS_KEY') }}"
s3_host_bucket: "https://{{ s3_bucket_name }}.s3.{{ s3_region }}.amazonaws.com"
```

## Example Playbook

``` yaml
- hosts: servers
  roles:
    - pgback
```
