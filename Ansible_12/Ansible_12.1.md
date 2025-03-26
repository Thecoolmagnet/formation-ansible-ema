# Ansible 12
## Exercice 1
### Configuration
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-14
vagrant up
vagrant ssh control
cd ansible/projets/ema/
```

Création playbook 1
```console
vim myvars1.yml
```
```yml
---  # myvars1.yml

- hosts: all
  gather_facts: false

  vars:
    mycar: alfa
    mybike: kawa

  tasks:
    - debug:
        msg: "My car: {{mycar}}, My bike: {{mybike}}"
```
Exécution du playbook
```console
ansible-playbook myvars1.yml
```
Exécution en remplaçant les variables
```console
ansible-playbook myvars1.yml -e mycar=bmw
ansible-playbook myvars1.yml -e mybike=ducati
ansible-playbook myvars1.yml -e mycar=bmw -e mybike=ducati
```

Création playbook 2
```console
vim myvars2.yml
```
```yml
---  # myvars2.yml

- hosts: all
  gather_facts: false

  tasks:
    - name: Define vars
      set_fact:
        mycar: alfa
        mybike: kawa
    - debug:
        msg: "My car: {{mycar}}, My bike: {{mybike}}"
```
Exécution du playbook
```console
ansible-playbook myvars2.yml
```
Exécution en remplaçant les variables
```console
ansible-playbook myvars2.yml -e mycar=bmw -e mybike=ducati
```

Création playbook 3
```console
vim myvars3.yml
```
```yml
---  # myvars3.yml

- hosts: all
  gather_facts: false

  tasks:
    - debug:
        msg: "My car: {{mycar}}, My bike: {{mybike}}"
```

Création des variables
```console
mkdir group_vars
```console
ansible-playbook myvars3.yml
```

Exécution du playbook
```console
ansible-playbook myvars3.yml
```









