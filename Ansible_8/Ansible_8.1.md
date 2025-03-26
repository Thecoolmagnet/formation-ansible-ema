# Ansible 8
## Exercice 1
### Configuration
Démarrage et connexion
```console
cd ~/formation-ansible/atelier-07
vagrant up
vagrant ssh ansible
cd ansible/projets/ema/
```

Installation des packets x2
```console
ansible all -m package -a "name=tree" && ansible all -m package -a "name=git" && ansible all -m package -a "name=nmap"
```
On remarque que pour la deuxième fois on passe à success car déjà installé

Désinstallation x2
```console
ansible all -m package -a "name=tree state=absent" && ansible all -m package -a "name=git state=absent" && ansible all -m package -a "name=nmap state=absent"
```
Même comportement

Copie x2
```console
ansible all -m copy -a "src=/etc/fstab dest=/tmp/test3.txt"
```

Suppression x2
```console 
ansible all -m file -a "dest=/tmp/test3.txt state=absent"
```

Espace disque x2
```console
ansible all -a "df -h /"
```
Il y a une rexécution de la commande

Fin propre
```console
exit
vagrant destroy -f
```
Suivant: [Partie 10](https://github.com/Thecoolmagnet/formation-ansible-ema/blob/main/Ansible_10/Ansible_10.1.md)
