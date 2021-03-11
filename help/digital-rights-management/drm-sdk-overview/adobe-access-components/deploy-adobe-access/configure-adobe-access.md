---
title: Distribuzione DRM di Adobe Primetime
description: Distribuzione DRM di Adobe Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Distribuire Adobe Primetime DRM {#configure-adobe-primetime-drm}

Un vantaggio chiave dell&#39;SDK DRM di Adobe Primetime è la possibilità di installarlo su qualsiasi server applicativo Java™ o contenitore servlet, come Tomcat. È inoltre necessario JDK™ 1.5 o versione successiva. Per ulteriori informazioni sui requisiti software, consulta Requisiti della piattaforma SDK DRM di Primetime: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

I passaggi di alto livello per implementare DRM di Primetime sono i seguenti:

1. Installa e configura Primetime DRM SDK.
1. Recuperare certificati digitali dall&#39;Adobe.
1. Crea un server licenze utilizzando l&#39;SDK o distribuisci il server DRM di Primetime per lo streaming protetto.
1. Crea strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri per creare pacchetti di contenuti, utilizza gli strumenti di preparazione dei contenuti forniti o concede la licenza a uno dei pacchetti Adobe HTTP Dynamic Streaming.
1. Definire le regole di utilizzo per il contenuto e creare criteri a supporto di tali regole.
1. Crea pacchetti di contenuti utilizzando gli strumenti di gestione dei pacchetti e dei criteri.
1. Sviluppa applicazioni video con cui i consumatori possono visualizzare i contenuti protetti utilizzando Flash Player o Adobe AIR oppure utilizza un OVP (Online Video Platform) stabilito che supporta Primetime DRM.
1. Distribuisci un file SWF da utilizzare con Flash Player sul tuo sito web o pubblica il programma di installazione di Adobe AIR per il download.

Questi passaggi vengono espansi nelle sezioni seguenti, con riferimenti ad altri documenti contenenti informazioni aggiuntive.

## Implementazione su un sistema operativo a 64 bit{#deploying-on-a-bit-operating-system}

Un sistema operativo a 64 bit, come la versione a 64 bit di RedHat o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

## Installare Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK viene fornito come file di archivio Java (JAR). Per ulteriori informazioni sull’installazione di DRM di Primetime, consulta Utilizzo dell’SDK DRM di Adobe Primetime per la protezione dei contenuti e le linee guida per la distribuzione sicura.

## Implementare un server licenze {#implement-a-license-server}

Utilizzando l’SDK DRM di Adobe Primetime, devi creare un server licenze. Quando il contenuto è protetto utilizzando DRM di Primetime, non può essere visualizzato finché non viene rilasciata una licenza al consumatore dal server licenze. Se si utilizza la licenza basata sull&#39;identità, l&#39;autenticazione basata sulla password assicura che solo i consumatori autorizzati possano aprire e visualizzare il contenuto.

Quando si implementa un server licenze, è necessario ottenere i certificati digitali necessari dall’Adobe. Per istruzioni dettagliate sulla richiesta dei certificati, consulta il documento Registrazione certificati DRM di Primetime .

Per ulteriori informazioni sull&#39;implementazione di un server licenze e sull&#39;ottenimento di certificati digitali, consulta **Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti.**

## Creare strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri{#create-content-packaging-and-policy-management-tools}

Utilizzando l’SDK DRM di Adobe Primetime, puoi creare strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri. Le API di gestione dei criteri consentono agli amministratori di creare, visualizzare i dettagli e aggiornare i criteri. Le API di packaging incorporano il criterio in un file video e lo crittografano utilizzando la chiave di crittografia del contenuto.

L&#39;SDK DRM di Primetime include un&#39;implementazione di riferimento ( [!DNL AdobePackager.jar]) che fornisce esempi di strumenti per la creazione di pacchetti di contenuti e la gestione dei criteri ( [!DNL AdobePolicyManager.jar]).

Per ulteriori informazioni sulla creazione di pacchetti di contenuti e strumenti di gestione dei criteri, consulta **Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti.**

## Creare criteri e contenuto del pacchetto {#create-policies-and-package-content}

Utilizzando le regole di utilizzo supportate dall’SDK, devi definire e creare criteri per supportare il modello di business della tua organizzazione, quindi creare pacchetti del contenuto utilizzando tali criteri. Una volta applicate le policy al contenuto durante l&#39;imballaggio, è possibile mantenere il controllo del contenuto indipendentemente dalla sua diffusione.

I criteri in Adobe Primetime DRM supportano un&#39;ampia gamma di regole di utilizzo diverse, tra cui:

* La specificazione del numero di giorni in cui una licenza è valida quando un consumatore inizia a guardare il contenuto.
* Consentire il caching delle licenze.
* Specifica dei runtime client e delle versioni in grado di accedere al contenuto (ad esempio, gli utenti devono disporre di una determinata applicazione Adobe AIR o di una specifica versione del Flash Player).
* Richiedere che i consumatori si autenticino utilizzando un nome utente e una password prima di visualizzare il contenuto protetto o consentire l&#39;accesso anonimo.

Per ulteriori informazioni sul contenuto del pacchetto, consulta *Protezione del contenuto*. Per ulteriori informazioni sulle regole di utilizzo e sui modelli di business supportati, consulta *Regole di utilizzo*.

## Sviluppare applicazioni per la riproduzione video {#develop-applications-for-video-playback}

Per consentire ai consumatori di accedere ai contenuti e visualizzarli, sviluppa un’applicazione di riproduzione video utilizzando Flash Player o Adobe AIR. Una volta sviluppata un’applicazione di riproduzione video, è necessario distribuirla ai consumatori. Se stai sviluppando un&#39;applicazione utilizzando il Flash Player, ospitala sul sito web dell&#39;organizzazione. Se stai sviluppando un’applicazione utilizzando Adobe® AIR®, pubblica il programma di installazione dell’applicazione AIR in modo che i consumatori possano scaricare e installare l’applicazione sul loro computer.

Per ulteriori informazioni sullo sviluppo di applicazioni di riproduzione video personalizzate da utilizzare con Adobe Primetime DRM, consulta il capitolo &quot;Utilizzo dei video&quot; nella [Guida per gli sviluppatori di ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), nel [Centro per la tecnologia video di Adobe](https://www.adobe.com/devnet/video/) e nel Open Source Media Framework.