# Ansible 3
## Installation
### Exercice 3
Initialisation de l'environnement de travail et connexion
```console
cd ~/formation-ansible/atelier-01
vagrant up rocky
vagrant ssh rocky
```

Installation pip 
```console
sudo dnf update
sudo dnf install python3-pip
python3 -m pip install --upgrade pip
```

Lancement venv
```console
python3 -m venv ~/.venv/ansible
source ~/.venv/ansible/bin/activate
```

Installation ansible dans le venv
```console
pip install ansible
ansible --version
```
La version d'Ansible est la 2.15.13

Fin propre
```console
deactivate
exit
vagrant destroy rocky
```
Suivant:  [Partie 4](https://github.com/Thecoolmagnet/formation-ansible-ema/blob/main/Ansible_4/Ansible_4.1.md)
