# Create-user-and-copy-ssh-ansible

```bash

---
 - name: cria o usuário nessus para as maquinas e exporta chave publica SSH
   hosts: jeff
   remote_user: root


   vars:
       user: nessus
       passwd: '00850'
       keypub: /home/nessus/.ssh/id_rsa.pub

   tasks:

    - name: criando usuário para scan do nessus
      user:
       name: '{{user}}'
       password: "{{ passwd | password_hash('sha256') }}"



    - name: copiando chave para hosts
      authorized_key:
       user: '{{user}}'
       key: "{{ lookup('file', '/home/nessus/.ssh/id_rsa.pub') }}"
       state: present



```
