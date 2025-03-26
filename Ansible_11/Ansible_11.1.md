# Ansible 11
## Exercice 1
### Configuration
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-12
vagrant up
vagrant ssh control
cd ansible/projets/ema/
cat inventory
```

Création du playbook chrony
```console
vim chrony.yml
```
```yml
---
- hosts: redhat
  become: yes
  tasks:
    - dnf:
        name: chrony
        state: present
    - copy:
        dest: "/etc/chrony.conf"
        content: |
            # /etc/chrony.conf
            server 0.fr.pool.ntp.org iburst
            server 1.fr.pool.ntp.org iburst
            server 2.fr.pool.ntp.org iburst
            server 3.fr.pool.ntp.org iburst
            driftfile /var/lib/chrony/drift
            makestep 1.0 3
            rtcsync
            logdir /var/log/chrony
        owner: root
        group: root
        mode: '0644'
      notify: Reload Chrony
  handlers:
    - name: Reload Chrony
      command:
        cmd: systemctl restart chronyd
```

Vérification du playbook
```console
yamllint chrony.yml
```

Exécution du playbook (x2)
```console
ansible-playbook chrony.yml
```



