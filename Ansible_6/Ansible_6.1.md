# Ansible 6
## Exercice 1
### Configuration
Démarrage des machines
```console
cd ~/formation-ansible/atelier-06
vagrant up
vagrant ssh control
```

Modification /etc/hosts
```console
sudo vim /etc/hosts
```
```console
192.168.56.10 control control
192.168.56.20 target01 target01
192.168.56.30 target02 target02
192.168.56.40 target03 target03
```

Création et copie de la clef ssh
```console
ssh-keygen
ssh-copy-id target0[1-3]
```

Installation d'ansible et test d'ansible
```console
sudo apt install ansible
ansible all -i target01,target02,target03 -m ping
```

Création de l'environnement de projet et test config
```console
mkdir ~/monprojet && cd monprojet && touch ansible.cfg
ansible --version | head -n 2
```

Ajout d'une conf basique (logs + fichier groupe)
```console
vim ansible.cfg
```
```console
[defaults]
inventory = ./hosts
log_path = ~/journal/ansible.log
```

Test des logs
```console
mkdir ../journal
ansible all -i target01,target02,target03 -m ping
cat ../journal/ansible.log
```

Création d'un groupe
```console
vim hosts
```
```console
[testlab]
target01
target02
target03

[testlab:vars]
ansible_user=vagrant
```
Test d'un ping
```console
ansible all -m ping
```

Permettre à ansible de passer sudo pour des actions nécessitant une élévation
```console
vim hosts
```
```console
"ansible_become=yes"
ansible all -a "head -n 1 /etc/shadow"
exit
```
