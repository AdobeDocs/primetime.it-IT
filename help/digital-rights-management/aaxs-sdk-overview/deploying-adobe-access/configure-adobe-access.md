---
seo-title: Distribuzione di Adobe Access
title: Distribuzione di Adobe Access
uuid: 9f9a9931-f607-4b1a-9209-0236a4c197ca
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Distribuzione di Adobe Access {#deploy-adobe-access}

Un vantaggio chiave di Adobe Access SDK è rappresentato dalla possibilità di installarlo in qualsiasi server applicazioni Java™ o contenitore servlet, ad esempio Tomcat. È inoltre necessario disporre di JDK™ 1.5 o versione successiva. Per ulteriori informazioni sui requisiti software, consulta Requisiti della piattaforma SDK di Adobe Access: [: https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

I passaggi di alto livello per implementare Adobe Access sono:

1. Installa e configura Adobe Access SDK.
1. Ottenete certificati digitali da Adobe.
1. Crea un server licenze con l’SDK o distribuisci Adobe Access Server per lo streaming protetto.
1. Create strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri per creare pacchetti di contenuti, utilizzate gli strumenti di preparazione dei contenuti forniti o fornite la licenza per uno dei pacchetti di streaming dinamico Adobe HTTP.
1. Definite le regole di utilizzo per il contenuto e create criteri a supporto di tali regole.
1. Create pacchetti di contenuti con gli strumenti di gestione dei pacchetti e dei criteri.
1. Sviluppare applicazioni video con cui i consumatori possano visualizzare il contenuto protetto tramite Flash Player o Adobe AIR oppure utilizzare un&#39;OVP (Piattaforma video online) già nota che supporta Adobe Access.
1. Potete implementare un file SWF da usare con Flash Player nel vostro sito Web oppure pubblicare il programma di installazione di Adobe AIR per il download.

Questi passaggi sono descritti nelle sezioni seguenti, con riferimenti ad altri documenti contenenti informazioni aggiuntive.

## Implementazione su un sistema operativo a 64 bit {#deploying-on-a-bit-operating-system}

Un sistema operativo a 64 bit, come la versione a 64 bit di RedHat o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

## Installare Adobe Access SDK {#install-adobe-access-sdk}

Adobe Access SDK viene fornito come file di archivio Java (JAR). Per ulteriori informazioni sull&#39;installazione di Adobe Access, vedere *Utilizzo di Adobe Access SDK per la protezione dei contenuti* e delle *linee guida* per la distribuzione protetta.

## Implementazione di un server licenze {#implement-a-license-server}

Con Adobe Access SDK, devi creare un server licenze. Quando il contenuto è protetto tramite Adobe Access, non può essere visualizzato finché non viene rilasciata una licenza al consumatore dal server licenze. Se si utilizza la licenza basata sull&#39;identità, l&#39;autenticazione basata sulla password assicura che solo i consumatori autorizzati possano aprire e visualizzare il contenuto.

Quando si implementa un server licenze, è necessario ottenere i certificati digitali necessari da Adobe. Per istruzioni dettagliate sulla richiesta dei certificati, fare riferimento al documento di registrazione dei certificati di Adobe Access.

Per ulteriori informazioni sull&#39;implementazione di un server licenze e sul recupero dei certificati digitali, vedere* Utilizzo di Adobe Access SDK per la protezione dei contenuti.*

## Creazione di pacchetti di contenuti e strumenti di gestione dei criteri {#create-content-packaging-and-policy-management-tools}

Con l’SDK di Adobe Access potete creare strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri. Le API di gestione dei criteri consentono agli amministratori di creare, visualizzare i dettagli e aggiornare i criteri. Le API di creazione pacchetti incorporano il criterio nel file FLV o F4V e cifrano il file utilizzando la chiave di crittografia del contenuto.

L’SDK di Adobe Access include un’implementazione di riferimento ( [!DNL AdobePackager.jar]) che fornisce esempi di strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri ( [!DNL AdobePolicyManager.jar]).

Per ulteriori informazioni sulla creazione di pacchetti di contenuti e strumenti di gestione dei criteri, consulta *Utilizzo di Adobe Access SDK per la protezione dei contenuti*.

## Creare criteri e creare pacchetti di contenuto {#create-policies-and-package-content}

Utilizzando le regole di utilizzo supportate dall&#39;SDK, devi definire e creare criteri a supporto del modello aziendale dell&#39;organizzazione, quindi creare pacchetti di contenuto utilizzando tali criteri. Una volta applicati i criteri al contenuto durante la creazione del pacchetto, potete mantenere il controllo del contenuto indipendentemente dalla sua estensione.

I criteri di Adobe Access supportano un&#39;ampia gamma di regole di utilizzo diverse, tra cui:

* Specifica del numero di giorni in cui una licenza è valida quando un consumatore inizia a guardare il contenuto.
* Consentire il caching delle licenze.
* Specifica dei runtime client e delle versioni in grado di accedere al contenuto (ad esempio, gli utenti devono disporre di una determinata applicazione Adobe AIR o di una versione specifica di Flash Player).
* Richiedere che i consumatori si autenticino utilizzando un nome utente e una password prima di visualizzare il contenuto protetto o consentire l&#39;accesso anonimo.

Per ulteriori informazioni sulla creazione di pacchetti di contenuti, consulta *Protezione dei contenuti*. Per ulteriori informazioni sulle regole di utilizzo e sui modelli di business che supportano, consulta Regole di *utilizzo*.

## Sviluppo di applicazioni per la riproduzione video {#develop-applications-for-video-playback}

Per consentire ai consumatori di accedere ai contenuti e visualizzarli, sviluppate un’applicazione di riproduzione video utilizzando Flash Player o Adobe AIR. Dopo aver sviluppato un’applicazione di riproduzione video, è necessario distribuirla ai consumatori. Se state sviluppando un&#39;applicazione con Flash Player, ospitatela sul sito Web dell&#39;organizzazione. Se state sviluppando un&#39;applicazione con Adobe® AIR®, inviate il programma di installazione dell&#39;applicazione AIR in modo che i consumatori possano scaricare e installare l&#39;applicazione sul computer.

Per ulteriori informazioni sullo sviluppo di applicazioni di riproduzione video personalizzate da utilizzare con Adobe Access, consultare il capitolo &quot;Working with Video&quot; nella Guida [per gli sviluppatori di](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)ActionScript 3.0*, *il Centro [per la tecnologia video](https://www.adobe.com/devnet/video/)Adobe e Open Source Media Framework.