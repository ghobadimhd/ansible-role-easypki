EeasyPKI
=========

This role create ssl certificate PKIs at remote hosts containing ca, server and clients certificates

Requirements
------------

**None**.

Role Variables
--------------

**TODO**

Dependencies
------------

**None**

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
---
- hosts: localhost
  roles:
    - role: easypki
      easypki_chains: 
        OpenVPN:
          root_dir: "{{ playbook_dir }}/pkis/OpenVPN"
          servers:
            openvpn:
              cn: OpenVPN
              not_after: "+365d"
              alt_names:
                domains: 
                  - ovpn.example.com
                ips:
                  - "{{ ansible_host }}"

          clients:
            client1:
              o: admin
              cn: admin
            client2:
              not_before: "+3d"
            client3:

        Company-root-ca:
          root_dir: "{{ playbook_dir }}/pkis/Company-root-ca"
          ca:
            filename: root
            cn: ROOT_CA
            o: example.com
            privatekey_size: 4096
            privatekey_passphrase: SECRET_PASS
          servers:
            website:
              cn: example.com
              privatekey_size: 4096
              privatekey_passphrase: SERVER_SECRET_PASS
              privatekey_cipher: aes256
              alt_names:
                domains: 
                  - example.com
                ips:
                  - "{{ ansible_host }}"
        all-vars:
          root_dir: "{{ playbook_dir }}/allvars-ca"
          ca: 
            directory_name: .
            filename: ca
            provider: selfsigned
            privatekey_size: 4096
            privatekey_cipher: aes256
            basic_constraints: CA:TRUE
            key_usage: 
              - keyCertSign
              - cRLSign
            extended_key_usage: []
            not_before: "+3d"
            not_after: "+1024d"

          servers:
            website:
              directory_name: servers
              provider: ownca
              privatekey_size: 2048
              privatekey_cipher: aes256
              key_usage: 
                - keyEncipherment
                - digitalSignature
                - keyAgreement
              extended_key_usage: 
                - serverAuth
              basic_constraints: CA:FALSE
              not_before: "+3d"
              not_after: "+1024d"

          clients:
            myClient:
              directory_name: clients
              provider: ownca
              privatekey_size: 1024
              privatekey_cipher: aes256
              key_usage: 
                - digitalSignature
                - keyAgreement
              extended_key_usage: 
                - clientAuth
              basic_constraints: CA:FALSE
              not_before: "+3d"
              not_after: "+1024d"
            
            mySecondClient:

        just-ca:

```

License
-------

MIT

Author Information
------------------

**Mohammad Ghobadi**

Mail: ghobadimhd@gmail.com
