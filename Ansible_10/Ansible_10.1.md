# Ansible 10
## Un serveur web simple
### Exercice 1
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-10
vagrant up
vagrant ssh ansible
cd ansible/projets/ema/
```

Création du playbook Debian
```console
vim apache-debian.yml
```
```yml
---
- hosts: debian
  become: yes
  tasks:
    - apt:
        update_cache: yes

    - apt:
        name: apache2
        state: present
    - copy:
        dest: "/var/www/html/index.html"
        content: |
            <html>
                <head>
                <title>Bienvenue sur mon serveur Apache</title>
                </head>
                <body>
                <h1>Bienvenue sur le serveur Apache configure via Ansible !</h1>
                <p>Ceci est une page personnalisee.</p>
                </body>
            </html>
        owner: root
        group: root
        mode: '0644'
```
Lancement du playbook
```console
ansible-playbook apache-debian.yml
```
Test de la page
```console
curl http://192.168.56.30
```

Playbook Rocky
```yml
---
- hosts: rocky
  become: yes
  tasks:
    - dnf:
        name: httpd
        state: present
    - copy:
        dest: "/var/www/html/index.html"
        content: |
            <html>
                <head>
                    <title>Bienvenue sur mon serveur Apache</title>
                </head>
                <body>
                    <h1>Bienvenue sur le serveur Apache configuré via Ansible !</h1>
                    <p>Ceci est une page personnalisée.</p>
                </body>
            </html>
        owner: root
        group: root
        mode: '0644'
```
Lancement du playbook
```console
ansible-playbook apache-rocky.yml
```
Test de la page
```console
curl http://192.168.56.20
```

Playbook Suse
```yml
---
- hosts: suse
  become: yes
  tasks:
    - zypper:
        name: apache2
        state: present
    - copy:
        dest: "/srv/www/htdocs/index.html"
        content: |
            <html>
                <head>
                    <title>Bienvenue sur mon serveur Apache</title>
                </head>
                <body>
                    <h1>Bienvenue sur le serveur Apache configure via Ansible !</h1>
                    <p>Ceci est une page personnalisee.</p>
                </body>
            </html>
        owner: root
        group: root
        mode: '0644'
``` 
Lancement du playbook
```console
ansible-playbook apache-suse.yml
```
Test de la page
```console
curl http://192.168.56.40
```

Fin propre
```console
exit
vagrant destroy -f
```
Suivant: [Partie 11 Handler](Ansible_11/Ansible_11.1.md)
