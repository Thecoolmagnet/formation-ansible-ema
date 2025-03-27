# Ansible 13
## Variables enregistrées
### Exercice 1
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-15
vagrant up
vagrant ssh control
cd ansible/projets/ema/
```

Création du playbook avec msg
```console
vim kernel.yml
```
```yml
---  # kernel.yml

- hosts: all
  gather_facts: false

  tasks:

    - name: Report kernel details
      command: uname -a
      changed_when: false
      register: df_cmd

    - debug:
        msg: "{{df_cmd.stdout_lines}}"
```

Exécution du playbook
```console
ansible-playbook kernel.yml
```

Modification du playbook avec vars
```console
vim kernel.yml
```
```yml
---  # kernel.yml

- hosts: all
  gather_facts: false

  tasks:

    - name: Report kernel details
      command: uname -a
      changed_when: false
      register: df_cmd

    - debug:
        var: df_cmd.stdout_lines
```

Exécution du playbook
```console
ansible-playbook kernel.yml
```

Création du playbook pour les host rocky et suse
```console
vim packages.yml
```
```yml
---  # kernel.yml

- hosts: packages
  gather_facts: false

  tasks:

    - name: Report number of packages
      shell: "rpm -qa | wc -l"
      changed_when: false
      register: df_cmd

    - debug:
        var: df_cmd.stdout_lines
```

Ajout du groupe packages
```console
vim inventory
```
```bash
[packages]
rocky
suse
```

Exécution du playbook
```console
ansible-playbook packages.yml
```

Fin propre
```console
exit
vagrant destroy -f
```
Suivant: [Partie 14 Facts et variables implicites](/Ansible_14/Ansible_14.1.md)
