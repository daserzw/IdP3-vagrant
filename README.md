# CORSO: INSTALLAZIONE E CONFIGURAZIONE DI SHIBBOLETH IDP V.3.3

Questo repository contiene un Vagrantfile per il Corso IDP NUOVI tenuto
in occasione degli IDEM DAY 2016 e per il nuovo corso di installazione
Shibboleth 3.3 che si terrà al WS GARR 2017:

https://www.idem.garr.it/idemday2016/separa-programma/6-giugno-corso-idp-nuovi

http://www.eventi.garr.it/it/ws17/programma/programma-esteso/corso-installazione-e-configurazione-di-shibboleth-idp-v-3-3#

## Requisiti

* vagrant: https://www.vagrantup.com/downloads.html
* VirtualBox: https://www.virtualbox.org/wiki/Downloads

## Istruzioni

Le istruzioni che seguono servono a:
- effettuare il provisioning della macchina virtuale con vagrant;
- installare e configurare i pacchetti necessari all'ambiente
  iniziale del corso tramite task ansible;
  
Nota: per certi portatili HP è stato necessario attivare a livello di BIOS l'opzione "Virtualization VT-x".
Prendere in considerazione questa soluzione qualora si incontrassero errori di accesso agli host virtuali
nei passi successivi.

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

**Eseguire dalla directory IdP3-vagrant**

Accedere alla macchina virtuale:

```
vagrant ssh
```

Una volta acceduti e ottenuto il prompt, eseguire:

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
contenuto e' conforme a quanto riportato.
**ATTENZIONE:** i certificati dei server sono firmati da una CA non
riconosciuta, quindi vanno accettati manualmente.

* LINK: https://idp.example.org
  CONTENUTO: `Virtualhost idp.example.org configurato correttamente`
* LINK: https://sp.example.org
  CONTENUTO: `Virtualhost sp.example.org configurato correttamente`
* LINK: https://idp.example.org/idp
  CONTENUTO: una pagina di errore di Apache Tomcat con contenuto `HTTP Status 404 - /idp`
* LINK: https://sp.example.org/secure
  CONTENUTO: una pagina dal titolo `shibsp::ConfigurationException`

Se tutti i contenuti sono conformi... COMPLIMENTI! Il provisioning e la
preparazione dell'ambiente iniziale per il corso sono andati a buon fine.


Se qualcosa e' andato storto segnalaci il problema rispondendo alla mail
di contatto o direttamente tramite le issues di github:
  https://github.com/daserzw/IdP3-vagrant/issues
 
