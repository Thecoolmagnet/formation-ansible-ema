# Ansible 14
## Exercice 1
### Configuration
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-16
vagrant up
vagrant ssh ansible
cd ansible/projets/ema/playbooks/
```

Création du premier playbook
```console
vim pkg-info.yml
```
```yml
---  # pkg-info.yml

- hosts: all

  tasks:

    - name: Display pakcet manager
      debug:
        msg: "{{ansible_host}}'s packet manager: {{ansible_pkg_mgr}}"
```

Exécution du playbook
```console
ansible-playbook pkg-info.yml
```

Création du deuxième playbook
```console
vim python-info.yml
```
```yml
---  # python-info.yml

- hosts: all

  tasks:

    - name: Display python version
      debug:
        msg: "{{ansible_host}}'s python version: {{ansible_python.version.major}}.{{ansible_python.version.minor}}.{{ansible_python.version.micro}}"
```

Exécution du playbook
```console
ansible-playbook python-info.yml
```

Création du troisième playbook
```console
vim dns-info.yml
```
```yml
---  # dns-info.yml

- hosts: all

  tasks:

    - name: Display DNS servers
      debug:
        msg: "{{ansible_host}}'s DNS servers: {{ansible_dns.nameservers}}"
```

Exécution du playbook
```console
ansible-playbook dns-info.yml
```

Fin propre
```console
exit
vagrant destroy -f
```
