# Ansible 15
## Cibles hétérogènes
### Exercice 1
Lancement de l'environnement et connexion
```console
cd ~/formation-ansible/atelier-17
vagrant up
vagrant ssh ansible
cd ansible/projets/ema/playbooks/
```

Création du playbook 1
```console
vim chrony-01.yml
```
```yml
---
- name: Installer et configurer Chrony avec modules natifs de gestion de paquets
  hosts:
    - debian
    - rocky
    - suse
    - ubuntu
  become: true

  tasks:
    - name: Installer Chrony sur Debian et Ubuntu (apt)
      apt:
        name: chrony
        state: present
      when: ansible_facts['distribution'] == 'Debian' or ansible_facts['distribution'] == 'Ubuntu'

    - name: Installer Chrony sur Rocky Linux (dnf)
      dnf:
        name: chrony
        state: present
      when: ansible_facts['distribution'] == 'Rocky'

    - name: Installer Chrony sur SUSE Linux (zypper)
      zypper:
        name: chrony
        state: present
      when: ansible_facts['distribution'] == 'openSUSE Leap'

    - name: Configurer le fichier chrony.conf sur suse et rocky
      copy:
        dest: "/etc/chrony/chrony.conf"
        content: |
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      when: ansible_distribution == "Debian" or ansible_distribution == "Ubuntu" 
      notify: Restart chrony service

    - name: Configurer le fichier chrony.conf sur suse et rocky
      copy:
        dest: "/etc/chrony.conf"
        content: |
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      when: ansible_distribution == "openSUSE Leap" or ansible_distribution == "Rocky" 
      notify: Restart chrony service

  handlers:
    - name: Restart chrony service
      command: systemctl restart chronyd
```

Exécution du playbook
```console
ansible-playbook chrony-01.yml
```

Création du playbook 2
```console
vim chrony-02.yml
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
      copy:
        dest: "{{ chrony_confdir }}"
        content: |
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      notify: Restart chrony service

  handlers:
    - name: Restart chrony service
      command: systemctl restart chronyd
```

Exécution du playbook
```console
ansible-playbook chrony-02.yml
```

Fin propre
```console
exit
vagrant destroy -f
```

Suivant: [Partie 16 Jinja & Templates](Ansible_16/Ansible_16.1.md)
