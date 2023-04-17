# ansible-role-win-restic-backup-jobs

Role to create Restic backup jobs and scripts in Windows Task Scheduler. Restic must be on PATH.

## Table of content

- [Default Variables](#default-variables)
  - [restic_backup_jobs](#restic_backup_jobs)
  - [restic_backup_jobs_enable](#restic_backup_jobs_enable)
  - [restic_backup_jobs_install_path](#restic_backup_jobs_install_path)
  - [restic_backup_jobs_password](#restic_backup_jobs_password)
  - [restic_backup_jobs_s3_bucket_name](#restic_backup_jobs_s3_bucket_name)
  - [restic_backup_jobs_s3_endpoint](#restic_backup_jobs_s3_endpoint)
  - [restic_backup_jobs_s3_repo](#restic_backup_jobs_s3_repo)
  - [restic_backup_jobs_s3_repo_access_key](#restic_backup_jobs_s3_repo_access_key)
  - [restic_backup_jobs_s3_repo_password](#restic_backup_jobs_s3_repo_password)
  - [restic_backup_jobs_s3_repo_secret_key](#restic_backup_jobs_s3_repo_secret_key)
  - [restic_backup_jobs_username](#restic_backup_jobs_username)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### restic_backup_jobs

Job definition

#### Default value

```YAML
restic_backup_jobs: []
```

#### Example usage

```YAML
restic_backup_jobs:
  - name: "dfs"
    description: "dfs files"
    dirs:
      - 'C:\test1'
    excludes:
      - Caches
      - Dbg*
      - Tempfile.txt
      - _temp
      - '*.tmp'
    triggers:
      - type: daily
        start_boundary: '2017-10-09T23:30:00'
    username: '{{ restic_backup_jobs_username }}'
    password: '{{ restic_backup_jobs_password }}'
    state: present
    enabled: no
    retention:
      keep_last: 1
      # keep_hourly: 1
      keep_daily: 7
      keep_weekly: 4
      # keep_monthly: 6
      # keep_yearly
```

### restic_backup_jobs_enable

Enable restic backup

#### Default value

```YAML
restic_backup_jobs_enable: false
```

### restic_backup_jobs_install_path

Path to store scripts

#### Default value

```YAML
restic_backup_jobs_install_path: '{{ ansible_env.ProgramFiles }}\restic_jobs'
```

### restic_backup_jobs_password

Password to run the backup job

#### Default value

```YAML
restic_backup_jobs_password: SomePassword1345
```

### restic_backup_jobs_s3_bucket_name

Minio S3 bucket name for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_bucket_name: restic-{{ inventory_hostname }}
```

### restic_backup_jobs_s3_endpoint

Minio S3 endpoint for restic backup storage

#### Default value

```YAML
restic_backup_jobs_s3_endpoint: '{{ backup__base__restic_s3_endpoint }}'
```

#### Example usage

```YAML
backup__base__restic_s3_endpoint: "https://minio.{{ dns_domain }}"
restic_backup_jobs_s3_endpoint: "{{ backup__base__restic_s3_endpoint }}"
```

### restic_backup_jobs_s3_repo

Minio S3 repo URL for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo: s3:{{ restic_backup_jobs_s3_endpoint }}/{{ restic_backup_jobs_s3_bucket_name
  }}
```

### restic_backup_jobs_s3_repo_access_key

Minio S3 repo access key for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo_access_key: '{{ backup__base__restic_s3_repo_access_key
  }}'
```

### restic_backup_jobs_s3_repo_password

Minio S3 repo password for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo_password: '{{ backup__base__restic_s3_repo_password }}'
```

### restic_backup_jobs_s3_repo_secret_key

Minio S3 repo secret key for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo_secret_key: '{{ backup__base__restic_s3_repo_secret_key
  }}'
```

### restic_backup_jobs_username

Username to run the backup jog

#### Default value

```YAML
restic_backup_jobs_username: administrator
```

## Discovered Tags

**_backup-init-restic_**\
&emsp;Init backup if restic is enabled.

**_backup-list-restic_**\
&emsp;List backups if restic is enabled.

**_backup-restic_**\
&emsp;Run backup if restic is enabled.

**_never_**

**_restore-restic_**\
&emsp;Run restore if restic is enabled.

**_restore-restic-single_**\
&emsp;Run single item restore if restic is enabled.


## Dependencies

None.

## License

license (GPL-2.0-or-later, MIT, etc)

## Author

andif888
