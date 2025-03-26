# Ansible 3
## Exercice 1
### Configuration
Initialisation de l'environnement de travail et connexion
```console
cd ~/formation-ansible/atelier-01
vagrant up ubuntu
vagrant ssh ubuntu
```

Recherche et installation d'Ansible
```console
sudo apt update
apt list ansible
sudo apt install ansible
```

Vérification de l'installation et de la version d'Ansible
```console
apt list --installed ansible
ansible --version
```
La version d'Ansible est la 2.10.8

Fin propre
```console
exit
vagrant destroy ubuntu
```

Suivant: [Exercice 2](https://github.com/Thecoolmagnet/formation-ansible-ema/blob/main/Ansible_3/Ansible_3.2.md)
