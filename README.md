# IDEM-IdP-Course
## Requisiti

* vagrant: https://www.vagrantup.com/downloads.html
* VirtualBox: https://www.virtualbox.org/wiki/Downloads

## Istruzioni

### Clonare il repository:
Aprire una finestra di terminale (cmd o powershell su windows):

```git clone https://github.com/daserzw/IDEM-IdP-Course.git```

### Istanziare la macchina virtuale con vagrant
(eseguire nella directory in cui si e' clonato il repository git)

```
cd IDEM-IdP-Course/vagrant
vagrant up
```

### Provisioning: eseguire il playbook di Ansible
(da eseguire dalla directory del repository: IDEM-IdP-Course)
```
cd vagrant
vagrant ssh
sudo su
cd /vagrant/ansible
ansible-playbook playbook.yml -i hosts
```

### Aggiungere IdP e SP al proprio hosts file

*Linux/Mac Os X*
```
cd /etc
```

*Windows*
```
cd %SystemRoot%\System32\drivers\etc\
```

*Tutti*
```
echo "10.0.3.2	idp.example.org" >> hosts
echo "10.0.4.2	sp.example.org" >> hosts
```

## Provisioning senza rete
Il primo provisioning della macchina virtuale deve necessariamente essere
effettuato in presenza del collegamento ad Internet. Successivamente, se
si vuole rilanciare ma non eseguendo i task che prevedono il collegamento
si puo' utilizzare il seguente comando:

```
cd /vagrant/ansible
ansible-playbook playbook.yaml -i hosts --skip-tags=online
```
