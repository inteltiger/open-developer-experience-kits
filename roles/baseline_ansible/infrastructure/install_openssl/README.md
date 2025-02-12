```text
SPDX-License-Identifier: Apache-2.0
Copyright (c) 2021 Intel Corporation
```

# Used global variables

Role requires following variables to be set:

- number_of_retries [int : 3]
- retry_delay [int : 1 ]
- project_dir [string : /opt/intel]
- project_user [string : {{ansible_user}}]
- project_group [string: {{ansible_user}} ]

# Certs locations in outher OSes

Based on https://golang.org/src/crypto/x509/root_linux.go

"/etc/ssl/certs",               // SLES10/SLES11
"/system/etc/security/cacerts", // Android
"/usr/local/share/certs",       // FreeBSD
"/etc/pki/tls/certs",           // Fedora/RHEL
"/etc/openssl/certs",           // NetBSD
"/var/ssl/certs",               // AIX

# Configuration

## Offline installation

```
  roles:
    - role: install_openssl
      offline_role: "{{ offline_enable | default(False) and ('controller_group' in group_names or single_node_deployment) }}"
      offline_openssl_download_url: "https://{{ hostvars[groups['controller_group'][0]]['ansible_host'] }}"
```
