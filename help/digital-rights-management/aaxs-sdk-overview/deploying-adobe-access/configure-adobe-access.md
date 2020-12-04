---
seo-title: Distribuzione  accesso al Adobe
title: Distribuzione  accesso al Adobe
uuid: 9f9a9931-f607-4b1a-9209-0236a4c197ca
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Distribuisci  accesso al Adobe {#deploy-adobe-access}

Un vantaggio fondamentale per  SDK di accesso al Adobe è rappresentato dalla possibilità di installarlo su qualsiasi server applicazioni Java™ o contenitore servlet, ad esempio Tomcat. È inoltre necessario disporre di JDK™ 1.5 o versione successiva. Per ulteriori informazioni sui requisiti software, consulta  requisiti di piattaforma SDK di accesso Adobe: [: https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

I passaggi di alto livello per distribuire  accesso al Adobe sono:

1. Installa e configura  Adobe Access SDK.
1. Ottenete certificati digitali da  Adobe.
1. Creare un server licenze utilizzando l&#39;SDK o distribuire Adobe Access Server per lo streaming protetto.
1. Create strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri per creare pacchetti di contenuti, utilizzate gli strumenti di preparazione dei contenuti forniti o fornite la licenza per uno dei pacchetti di HTTP Dynamic Streaming di Adobe .
1. Definite le regole di utilizzo per il contenuto e create criteri a supporto di tali regole.
1. Create pacchetti di contenuti con gli strumenti di gestione dei pacchetti e dei criteri.
1. Sviluppare applicazioni video con cui i consumatori possano visualizzare i contenuti protetti utilizzando l&#39;Flash Player o  Adobe AIR, oppure utilizzare un&#39;OVP (Piattaforma video online) già esistente che supporti  accesso Adobe.
1. Distribuite un file SWF da usare con il Flash Player sul vostro sito Web oppure pubblicate il programma di installazione di Adobe AIR  per il download.

Questi passaggi sono descritti nelle sezioni seguenti, con riferimenti ad altri documenti contenenti informazioni aggiuntive.

## Implementazione su un sistema operativo a 64 bit {#deploying-on-a-bit-operating-system}

Un sistema operativo a 64 bit, come la versione a 64 bit di RedHat o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

## Installa  SDK di accesso al Adobe {#install-adobe-access-sdk}

 Adobe Access SDK viene fornito come file di archivio Java (JAR). Per ulteriori informazioni sull&#39;installazione  accesso al Adobe, vedere *Utilizzo  SDK di accesso al Adobe per la protezione dei contenuti* e *Linee guida per la distribuzione protetta*.

## Implementazione di un server licenze {#implement-a-license-server}

Utilizzando  Adobe Access SDK, è necessario creare un server licenze. Se il contenuto è protetto tramite  accesso al Adobe, non può essere visualizzato finché non viene rilasciata una licenza al consumatore dal server licenze. Se si utilizza la licenza basata sull&#39;identità, l&#39;autenticazione basata sulla password assicura che solo i consumatori autorizzati possano aprire e visualizzare il contenuto.

Quando si implementa un server licenze, è necessario ottenere i certificati digitali necessari da  Adobe. Per istruzioni dettagliate sulla richiesta di certificati, fare riferimento al documento di iscrizione  certificato di accesso al Adobe.

Per ulteriori informazioni sull&#39;implementazione di un server licenze e sul recupero dei certificati digitali, vedere* Utilizzo di  SDK di accesso ai Adobi per la protezione dei contenuti.*

## Creare pacchetti di contenuti e strumenti di gestione dei criteri {#create-content-packaging-and-policy-management-tools}

Utilizzando l&#39;SDK di accesso al Adobe  potete creare la creazione di pacchetti di contenuti e strumenti di gestione dei criteri. Le API di gestione dei criteri consentono agli amministratori di creare, visualizzare i dettagli e aggiornare i criteri. Le API di creazione pacchetti incorporano il criterio nel file FLV o F4V e cifrano il file utilizzando la chiave di crittografia del contenuto.

L&#39;SDK di accesso al Adobe  include un&#39;implementazione di riferimento ( [!DNL AdobePackager.jar]) che fornisce esempi di strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri ( [!DNL AdobePolicyManager.jar]).

Per ulteriori informazioni sulla creazione di pacchetti di contenuti e strumenti di gestione dei criteri, consultate *Utilizzo dell&#39;SDK di accesso ai Adobi  per la protezione dei contenuti*.

## Creare criteri e creare pacchetti di contenuto {#create-policies-and-package-content}

Utilizzando le regole di utilizzo supportate dall&#39;SDK, devi definire e creare criteri a supporto del modello aziendale dell&#39;organizzazione, quindi creare pacchetti di contenuto utilizzando tali criteri. Una volta applicati i criteri al contenuto durante la creazione del pacchetto, potete mantenere il controllo del contenuto indipendentemente dalla sua estensione.

I criteri in  Accesso Adobe supportano un&#39;ampia gamma di regole di utilizzo diverse, tra cui:

* Specifica del numero di giorni in cui una licenza è valida quando un consumatore inizia a guardare il contenuto.
* Consentire il caching delle licenze.
* Specifica dei runtime client e delle versioni in grado di accedere al contenuto (ad esempio, gli utenti devono disporre di una determinata applicazione Adobe AIR  o di una versione specifica del Flash Player).
* Richiedere che i consumatori si autenticino utilizzando un nome utente e una password prima di visualizzare il contenuto protetto o consentire l&#39;accesso anonimo.

Per ulteriori informazioni sulla creazione di pacchetti di contenuti, vedere *Protezione dei contenuti*. Per ulteriori informazioni sulle regole di utilizzo e sui modelli aziendali supportati, vedere *Regole di utilizzo*.

## Sviluppo di applicazioni per la riproduzione video {#develop-applications-for-video-playback}

Per consentire ai consumatori di accedere ai contenuti e visualizzarli, sviluppate un’applicazione di riproduzione video utilizzando l’Flash Player o  Adobe AIR. Dopo aver sviluppato un’applicazione di riproduzione video, è necessario distribuirla ai consumatori. Se state sviluppando un&#39;applicazione utilizzando il Flash Player, ospitatela sul sito Web dell&#39;organizzazione. Se state sviluppando un&#39;applicazione utilizzando  Adobe® AIR®, inviate il programma di installazione dell&#39;applicazione AIR in modo che i consumatori possano scaricare e installare l&#39;applicazione sul loro computer.

Per ulteriori informazioni sullo sviluppo di applicazioni di riproduzione video personalizzate da utilizzare con  accesso al Adobe, vedere il capitolo &quot;Utilizzo del video&quot; nella [ Guida per sviluppatori di ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*, *il [ Adobe Centro per la tecnologia video il](https://www.adobe.com/devnet/video/) e il Open Source Media Framework.