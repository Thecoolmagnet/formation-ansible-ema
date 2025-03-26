# Ansible 4
## Exercice 1
### Configuration
Démarrage de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-03
vagrant up
vagrant ssh control
```

Vérification de l'installation d'ansible
```console
type ansible
```

Ajout des targets dans /etc/hosts
```console
sudo vim /etc/hosts
```
```bash
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

Ping ansible
```console
Création et copie de la clef ssh
```console
ssh-keygen
ssh-copy-id target0[1-3]
```

Fin propre
```console
exit
vagrant destroy -f
```
Suivant: [Partie 6](https://github.com/Thecoolmagnet/formation-ansible-ema/blob/main/Ansible_6/Ansible_6.1.md)
