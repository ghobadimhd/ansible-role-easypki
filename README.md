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
        - name: OpenVPN
          root_dir: "{{ playbook_dir }}/pkis"
          ca:
            name: ca
          servers:
            - name: openvpn
              cn: OpenVPN
              alt_names:
                domains: 
                  - ovpn.example.com
                ips:
                  - "{{ ansible_host }}"

          clients:
            - name: client1
              o: admin
              cn: admin
            - name: client2
            - name: client3

        - name: Company-root-ca
          root_dir: "{{ playbook_dir }}/pkis"
          ca:
            name: root
            cn: ROOT_CA
            o: example.com
            privatekey_size: 4096
            privatekey_passphrase: SECRET_PASS
          servers:
            - name: website
              cn: example.com
              privatekey_size: 4096
              privatekey_passphrase: SERVER_SECRET_PASS
              privatekey_cipher: aes256
              alt_names:
                domains: 
                  - example.com
                ips:
                  - "{{ ansible_host }}"

```

License
-------

MIT

Author Information
------------------

**Mohammad Ghobadi**

Mail: ghobadimhd@gmail.com
