# CORSO: INSTALLAZIONE E CONFIGURAZIONE DI SHIBBOLETH IDP V.3.3.X

Questo repository contiene un Vagrantfile per il corso di Installazione e configurazione di base di uno Shibboleth Identity Provider v3.3.x tramite ansible tenuto
in occasione degli IDEM DAY 2018:

https://learning.garr.it/enrol/index.php?id=45

## Requisiti

* Vagrant: https://www.vagrantup.com/downloads.html (Testato con le versioni 2.0.3 e v2.0.4)
* VirtualBox: https://www.virtualbox.org/wiki/Downloads (Testato con la versione v5.2.8 e v5.2.10)

## Istruzioni

Le istruzioni che seguono servono a:
- effettuare il provisioning della macchina virtuale con vagrant;
- installare e configurare i pacchetti necessari all'ambiente
  iniziale del corso tramite task ansible;
  
Nota: per certi portatili HP è stato necessario attivare a livello di BIOS l'opzione "Virtualization VT-x".
Prendere in considerazione questa soluzione qualora si incontrassero errori di accesso agli host virtuali
nei passi successivi.

### Provisioning: macchina virtuale

## Istructions for Linux

1. Recuperare il repository GIT del corso:
   * ```sudo su -```
   * ```apt install git```
   * ```cd /opt/ ; git clone https://github.com/ConsortiumGARR/IdP3-vagrant.git``` 

2. Spostarsi sulla cartella "```IdP3-vagrant```":
   * ```cd /opt/IdP3-vagrant```

3. Installare le Guest Additions di Virtualbox con "```vagrant plugin install vagrant-vbguest```"

4. Installare il plugin di Vagrant per ridimensionare l'hard disk per il corso a 10 GB: "```vagrant plugin install vagrant-disksize```"

5. Eseguire "```vagrant up```" per istanziare l'ambiente di sviluppo del corso.

6. Accedere alla VM del corso eseguendo il comando ```vagrant ssh``` dalla cartella ```/opt/IdP3-vagrant```

7. Una volta acceduti e ottenuto il prompt, eseguire:

   ```bash
      sudo su -
      git clone https://github.com/ConsortiumGARR/IdP3-ansible.git
      cd IdP3-ansible
      ansible-playbook playbook.yml -i hosts
   ```

8. Cambiare il proprio "```/etc/hosts```" (Linux) aggiungendo la seguente linea:
   ```bash
      192.168.33.10  idp.example.org sp.example.org idp sp
   ```

9. Ora è possibile accedere alla VM del corso mediante l'IP (```192.168.33.10```) o il nome (```idp.example.org``` o ```sp.example.org```) e protrete vedere le applicazioni web usate durante il corso sul vostro browser preferito (Chrome, FireFox, Opera, ...)

## Istructions for MacOSX

1. Recuperare il repository GIT del corso:
   * ```cd Desktop ; git clone https://github.com/ConsortiumGARR/IdP3-vagrant``` 

2. Spostarsi sulla cartella "```IdP3-vagrant```":
   * ```cd /opt/IdP3-vagrant```

3. Installare le Guest Additions di Virtualbox con "```vagrant plugin install vagrant-vbguest```"

4. Installare il plugin di Vagrant per ridimensionare l'hard disk per il corso a 10 GB: "```vagrant plugin install vagrant-disksize```"

5. Eseguire "```vagrant up```" per istanziare l'ambiente di sviluppo del corso.

6. Accedere alla VM del corso eseguendo il comando ```vagrant ssh``` dalla cartella ```/opt/IdP3-vagrant```

7. Una volta acceduti e ottenuto il prompt, eseguire:

   ```bash
      sudo su -
      git clone https://github.com/ConsortiumGARR/IdP3-ansible.git
      cd IdP3-ansible
      ansible-playbook playbook.yml -i hosts
   ```

8. Cambiare il proprio "```/etc/hosts```" (Linux) aggiungendo la seguente linea:
   ```bash
      192.168.33.10  idp.example.org sp.example.org idp sp
   ```

9. Ora è possibile accedere alla VM del corso mediante l'IP (```192.168.33.10```) o il nome (```idp.example.org``` o ```sp.example.org```) e protrete vedere le applicazioni web usate durante il corso sul vostro browser preferito (Chrome, FireFox, Opera, ...)

## Istructions for Windows

1. Installare GIT prelevando il setup da: ```https://git-scm.com/download/win``` (scegliere "Vim" come GIT default editor, "Use GIT from Git Bash only", "Use OpenSSL library, "Checkout Windows style", "Use MinTTY" e lasciare quanto è già selezionato di default se non si sa cosa scegliere)
```
2. Avviare la Git Bash al termine dell'installazione

3. Recuperare il repository GIT del corso:
   * ```git clone https://github.com/ConsortiumGARR/IdP3-vagrant.git``` 

4. Spostarsi sulla cartella "```IdP3-vagrant```":
   * ```cd /opt/IdP3-vagrant```

5. Installare le Guest Additions di Virtualbox con "```vagrant plugin install vagrant-vbguest```"

6. Installare il plugin di Vagrant per ridimensionare l'hard disk per il corso a 10 GB: "```vagrant plugin install vagrant-disksize```"

7. Eseguire "```vagrant up```" per istanziare l'ambiente di sviluppo del corso.

8. Accedere alla VM del corso eseguendo il comando ```vagrant ssh``` dalla cartella ```/opt/IdP3-vagrant```.

9. Una volta acceduti e ottenuto il prompt, eseguire:

   ```bash
      sudo su -
      git clone https://github.com/ConsortiumGARR/IdP3-ansible.git
      cd IdP3-ansible
      ansible-playbook playbook.yml -i hosts
   ```

10. Cambiare il proprio "```C:\Windows\System32\drivers\etc\hosts```" (Windows) aggiungendo la seguente linea:
   ```bash
      192.168.33.10  idp.example.org sp.example.org idp sp
   ```

11. Ora è possibile accedere alla VM del corso mediante l'IP (```192.168.33.10```) o il nome (```idp.example.org``` o ```sp.example.org```) e protrete vedere le applicazioni web usate durante il corso sul vostro browser preferito (Chrome, FireFox, Opera, ...)


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
  https://github.com/ConsortiumGARR/IdP3-vagrant/issues
