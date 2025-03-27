# Ansible 3
## Installation
### Exercice 2
Initialisation de l'environnement de travail et connexion
```console
cd ~/formation-ansible/atelier-01
vagrant up ubuntu
vagrant ssh ubuntu
```

Ajout du repo
```console
sudo apt update
sudo apt-add-repository ppa:ansible/ansible
```

Recherche et installation d'Ansible
```console
apt list ansible
sudo apt install ansible
```

Vérification de l'installation et de la version d'Ansible
```console
apt list --installed ansible
ansible --version
```
La version d'Ansible est la 2.17

Fin propre
```console
exit
vagrant destroy ubuntu
```
Suivant:  [Exercice 3](Ansible_3.3.md)
