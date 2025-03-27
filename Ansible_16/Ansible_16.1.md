# Ansible 16
## Jinja & Templates
### Exercice 1
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-18
vagrant up
vagrant ssh ansible
cd ansible/projets/ema/playbooks/
```

Création du playbook
```console
vim chrony.yml
```
```yml
---
- name: Installer et configurer Chrony avec module packages
  hosts:
    - debian
    - rocky
    - suse
    - ubuntu
  become: true

  tasks:
    - name: Installer le paquet Chrony
      package:
        name: chrony
        state: present

    - name: Définir les variables
      set_fact:
        chrony_confdir: /etc/chrony/chrony.conf
        when: ansible_distribution in ["Debian", "Ubuntu"]

      set_fact:
        chrony_confdir: /etc/chrony.conf
        when: ansible_distribution in ["Rocky", "openSUSE Leap"]

    - name: Configurer le fichier chrony.conf
      template:
        src: "chrony.conf.j2"
        dest: "{{ chrony_confdir }}"
        owner: root
        group: root
        mode: '0644'
      notify: Restart chrony service

    - name : Vérification
      shell: cat "{{ chrony_confdir }}" | head -n 1
      register: chrony_conf

    - name: Affichage vérif
      debug:
        msg: "{{ chrony_conf.stdout }}"

  handlers:
    - name: Restart chrony service
      command: systemctl restart chronyd
```

Création de la template
```console
vim templates/chrony.conf.j2
```
```bash
# Fichier est généré par Ansible. Le chemin complet est : {{ chrony_confdir }}
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst
driftfile /var/lib/chrony/drift
makestep 1.0 3
rtcsync
logdir /var/log/chrony
```

Exécution du playbook
```console
ansible-playbook chrony.yml
```

Fin propre
```console
exit
vagrant destroy -f
```

[Retour à la première partie](https://github.com/Thecoolmagnet/formation-ansible-ema/blob/main/Ansible_3/Ansible_3.1.md)
