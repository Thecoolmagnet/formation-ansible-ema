# Ansible 3
## Exercice 3
### Configuration
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
