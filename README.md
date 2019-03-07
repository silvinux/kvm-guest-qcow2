Role Name
=========

Ansible role to create a KVM guest from a qcow2 image.

Requirements
------------

This role is tested on Ansible 2.7.7, and platform requirements are listed in the metadata file.

Role Variables
--------------
```
      vm_location: "/var/lib/libvirt/images"
      image: "/home/silvinux/kvm/rhel-server-7.6-x86_64-kvm.qcow2"
      path_output: "/var/log/cloud-init.log"
      new_image_size: "40G"
      dir_owner: silvinux
      dir_group: silvinux
      env_LIBGUESTFS_BACKEND: "direct"
      preallocation: metadata
      ssh_keys:
        - sshkey: ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICoT3oooouuuuVOFktOj+rGFhqlxdr0bNH+ln7cDLJtH silvio@silvinux.example.com
      users_dic:
        - name: student
          groups: users,wheel
          shell: /bin/bash
          sudo: ALL=(ALL) NOPASSWD:ALL
      chg_pwd_users:
        - name: root
          password: toor
        - name: student
          password: redhat
      timezone: "Europe/Madrid"
      guests:
        test:
          fqdn: test.example.com
          mem: 512
          cpus: 1
          os_type: rhel7
          file_type: qcow2
          network: "bridge=virbr0"
          model: virtio
          graphics: spice
          address: 192.168.122.12
          network: 192.168.122.0
          netmask: 255.255.255.0
          broadcast: 192.168.122.255
          gateway: 192.168.122.1
```

Dependencies
------------
N/A

Example Playbook
----------------
```
   - hosts: local
     gather_facts: yes
     connection: local
     become: yes
     become_method: sudo
     environment:
       LIBGUESTFS_BACKEND: direct
     roles:
       - role: kvm
         vm_location: "/var/lib/libvirt/images"
         image: "/home/silvinux/kvm/rhel-server-7.6-x86_64-kvm.qcow2"
         path_output: "/var/log/cloud-init.log"
         new_image_size: "10G"
         dir_owner: silvinux 
         dir_group: silvinux 
         env_LIBGUESTFS_BACKEND: "direct"
         preallocation: metadata
         ssh_keys:
           - sshkey: ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICoT3oooouuuuVOFktOj+rGFhqlxdr0bNH+ln7cDLJtH silvio@silvinux.example.com
         users_dic:
           - name: student
             groups: users,wheel
             shell: /bin/bash
             sudo: ALL=(ALL) NOPASSWD:ALL
         chg_pwd_users:
           - name: root
             password: toor
           - name: student
             password: redhat
         timezone: "Europe/Madrid"
         guests:
           idm:
             fqdn: idm.lab.example.com
             mem: 512
             cpus: 1
             os_type: rhel7
             file_type: qcow2
             network: "bridge=virbr0"
             model: virtio
             graphics: spice
             address: 192.168.122.13
             network: 192.168.122.0
             netmask: 255.255.255.0
             broadcast: 192.168.122.255
             gateway: 192.168.122.1
```
License
-------

GPLv3

Author Information
------------------
silvinux - silvinux7@gmail.com
