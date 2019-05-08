# Ansible-script-to-grant-revoke-ssh-access

This script can be use to add a new user and provide him with both password based and key based authentication.

Usage:

When ever an ssh access has to be given to a new user or revoke the access for an existing user you will have to edit the main.yml file in the vars directory.

To create user with ssh access:

Add the user with the details specified as per the formats in the file.

user:
  comment: "abc user"
  group: developers
  password: encrypted password
  shell: /bin/bash
  remove: no
  state: present
  key: "{{ lookup('file', 'username_rsa.pub') }}"

  To encrypt the password you can follow either of the below methods. Password is optional.

  1) https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module
  2) Use perl -e 'print crypt("your password here", "pepper"),"\n"'

In order to revoke the access just change the remove option to yes and state to absent.

user:
  comment: "abc user"
  group: developers
  password: encrypted password
  shell: /bin/bash
  remove: yes
  state: absent
  key: "{{ lookup('file', 'username_rsa.pub') }}"


To run the playbook execute the below command:

ansible-playbook -i inventory/ add_users.yml
