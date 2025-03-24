# Ansible 3
## Exercice 3
### Configuration
cd ~/formation-ansible/atelier-01

vagrant up rocky

vagrant ssh rocky

sudo dnf update

sudo dnf install python3-pip

python3 -m pip install --upgrade pip

python3 -m venv ~/.venv/ansible

source ~/.venv/ansible/bin/activate

pip install ansible

ansible --version (2.15.13)

deactivate

exit

vagrant destroy rocky
