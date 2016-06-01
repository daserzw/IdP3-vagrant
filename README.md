# IDEM-IdP-Course

## Requisiti

* vagrant: https://www.vagrantup.com/downloads.html
* VirtualBox: https://www.virtualbox.org/wiki/Downloads

## Istruzioni

Le istruzioni che seguono servono a:
- effettuare il provisioning della macchina virtuale con vagrant;
- installare e configurare i pacchetti necessari all'ambiente
  iniziale del corso tramite task ansible;

### Provisioning: macchina virtuale

Scaricare e scompattare il file ZIP contenente il Vagrantfile da:
	  
 https://github.com/daserzw/IdP3-vagrant/archive/master.zip

Aprire una finestra di terminale (cmd o powershell su windows) e
posizionarsi nella directory in cui si e' scompattato il file ZIP:

```
cd IdP3-vagrant
vagrant up
```

### Clonare il repository git con i task ansible

**Eseguire dalla directory `IdP3-vagrant`**

Entrare nella macchina virtuale
```
vagrant ssh
```

Una volta ottenuto il prompt della macchina virtuale
eseguire i seguenti comandi:

```
sudo su -
git clone https://github.com/daserzw/IdP3-ansible.git
cd IdP3-ansible
ansible-playbook playbook.yml -i hosts
```

### Aggiungere IdP e SP al proprio hosts file

**Da eseguire sul computer su cui girano Virtualbox e vagrant**

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

### Verifica

**Da eseguire sul computer su cui girano Virtualbox e vagrant**

Aprire un browser, seguire i link che seguono e verificare se il
contenuto e' conforme a quanto riportato:

* LINK: https://idp.example.org
  CONTENUTO: `Virtualhost idp.example.org configurato correttamente`
* LINK: https://sp.example.org
  CONTENUTO: `Virtualhost sp.example.org configurato correttamente`
* LINK: https://idp.example.org
  CONTENUTO: una pagina di errore di Apache Tomcat con contenuto `HTTP Status 404 - /idp`
* LINK: https://idp.example.org/idp
  CONTENUTO: una pagina dal titolo `shibsp::ConfigurationException`

Se tutti i contenuti sono conformi... COMPLIMENTI! Il provisioning e la
preparazione dell'ambiente iniziale per il corso sono andati a buon fine.


Se qualcosa e' andato storto segnalaci il problema tramite le issues di github:
  https://github.com/daserzw/IdP3-vagrant/issues
 