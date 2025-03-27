# Ansible 12
## Variables
### Exercice 1
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

Création des variables pas défaut
```console
mkdir group_vars
vim group_vars/all.yml
```
```yml
---  # group_vars/all.yml

mycar: VW
mybike: BMW
```
Exécution du playbook
```console
ansible-playbook myvars3.yml
```

Modification du la variable pour target02
```console
mkdir host_vars
vim host_vars/target02.yml
```
```yml
---  # host_vars/target02.yml

mycar: Mercedes
mybike: Honda
```

Exécution du playbook
```console
ansible-playbook myvars3.yml
```

Création playbook 4
```console
vim display_user.yml
```
```yml
---  # display_user.yml

- hosts: all
  gather_facts: false

  vars_prompt:

    - name: user
      prompt: Enter username
      default: microlinux
      private: false

    - name: password
      prompt: Enter password (secret)
      default: yatahongaga
      private: true

  tasks:
    - debug:
        msg: "User is {{user}}, password is {{password}}"

```

Exécution du playbook
```console
ansible-playbook display_user.yml
```

Fin propre
```console
exit
vagrant destroy -f
```
Suivant: [Partie 13](https://github.com/Thecoolmagnet/formation-ansible-ema/blob/main/Ansible_13/Ansible_13.1.md)
