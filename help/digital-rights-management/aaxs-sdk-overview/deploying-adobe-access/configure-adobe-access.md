---
title: Distribuire l’accesso agli Adobi
description: Distribuire l’accesso agli Adobi
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Distribuire l’accesso agli Adobi {#deploy-adobe-access}

Un vantaggio chiave dell’SDK di Access di Adobe è la possibilità di installarlo su qualsiasi server applicazioni Java™ o contenitore di servlet, ad esempio Tomcat. È inoltre necessario JDK™ 1.5 o versione successiva. Per ulteriori informazioni sui requisiti software, consulta l’Adobe Requisiti della piattaforma SDK per l’accesso: [: https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

I passaggi di alto livello per distribuire l’accesso Adobe sono i seguenti:

1. Installa e configura l’SDK di accesso Adobe.
1. Ottieni certificati digitali da Adobe.
1. Creare un server licenze utilizzando l&#39;SDK o distribuire Adobe Access Server for Protected Streaming.
1. Creazione di pacchetti di contenuti e strumenti di gestione delle policy per creare pacchetti di contenuti, utilizzare gli strumenti di preparazione dei contenuti forniti o concedere in licenza uno dei pacchetti Adobe HTTP Dynamic Streaming.
1. Definisci le regole di utilizzo per il contenuto e crea criteri a supporto di tali regole.
1. Crea pacchetti dei contenuti utilizzando gli strumenti di gestione dei pacchetti e delle policy.
1. Sviluppa applicazioni video con le quali i consumatori possono visualizzare i contenuti protetti utilizzando il Flash Player o Adobe AIR, oppure utilizza una OVP (Online Video Platform) consolidata che supporta l’accesso agli Adobi.
1. Distribuisci un file SWF da utilizzare con il Flash Player sul tuo sito Web o pubblica il programma di installazione di Adobe AIR per il download.

Questi passaggi sono descritti nelle sezioni seguenti, con riferimenti ad altri documenti che contengono informazioni aggiuntive.

## Distribuzione su un sistema operativo a 64 bit {#deploying-on-a-bit-operating-system}

Un sistema operativo a 64 bit, come la versione a 64 bit di RedHat o Windows, offre prestazioni molto migliori rispetto a un sistema operativo a 32 bit.

## Installare l’SDK per l’accesso agli Adobi {#install-adobe-access-sdk}

L’SDK di accesso Adobe viene fornito come file di archivio Java (JAR). Per ulteriori informazioni sull&#39;installazione di Adobe Access, vedere *Utilizzo dell’SDK per l’accesso agli Adobi per proteggere i contenuti* e *Linee guida per la distribuzione sicura*.

## Implementare un server licenze {#implement-a-license-server}

Con l’SDK di Adobe Access è necessario creare un server licenze. Quando il contenuto è protetto con Adobe Access, non può essere visualizzato finché non viene rilasciata una licenza al consumatore dal server licenze. Se si utilizzano licenze basate su identità, l’autenticazione basata su password garantisce che solo i consumatori autorizzati possano aprire e visualizzare il contenuto.

Quando si implementa un server licenze, è necessario ottenere i certificati digitali necessari da Adobe. Per istruzioni dettagliate sulla richiesta dei certificati, consulta il documento di registrazione dei certificati di accesso Adobe.

Per ulteriori informazioni sull’implementazione di un server licenze e sull’ottenimento di certificati digitali, consulta* Utilizzo dell’SDK di accesso Adobe per la protezione dei contenuti.*

## Creare pacchetti di contenuti e strumenti di gestione delle policy {#create-content-packaging-and-policy-management-tools}

Utilizzando l’SDK di accesso di Adobe, puoi creare pacchetti di contenuti e strumenti di gestione delle policy. Le API di gestione dei criteri consentono agli amministratori di creare, visualizzare i dettagli e aggiornare i criteri. Le API di creazione pacchetti incorporano la policy nel file FLV o F4V e crittografano il file utilizzando la chiave di crittografia del contenuto.

L’SDK di accesso di Adobe include un’implementazione di riferimento ( [!DNL AdobePackager.jar]) che fornisce esempi di packaging dei contenuti e strumenti di gestione delle policy ( [!DNL AdobePolicyManager.jar]).

Per ulteriori informazioni sulla creazione di pacchetti di contenuti e sugli strumenti di gestione delle policy, consulta *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti*.

## Creare criteri e contenuti del pacchetto {#create-policies-and-package-content}

Utilizzando le regole di utilizzo supportate dall’SDK, devi definire e creare criteri a supporto del modello di business della tua organizzazione, quindi creare un pacchetto dei contenuti utilizzando tali criteri. Una volta applicate le policy ai contenuti durante la creazione dei pacchetti, puoi mantenere il controllo dei contenuti, indipendentemente dalla loro diffusione.

I criteri di accesso Adobe supportano un&#39;ampia gamma di regole di utilizzo diverse, tra cui:

* Specifica il numero di giorni di validità di una licenza quando un consumatore inizia a guardare il contenuto.
* Consentire il caching delle licenze.
* Specifica i runtime client e le versioni che possono accedere al contenuto (ad esempio, gli utenti devono avere una determinata applicazione Adobe AIR o una versione specifica del Flash Player).
* Richiedere che i consumatori si autentichino utilizzando un nome utente e una password prima di visualizzare contenuto protetto o consentire l’accesso anonimo.

Per ulteriori informazioni sulla creazione di pacchetti di contenuti, consulta *Protezione dei contenuti*. Per ulteriori informazioni sulle regole di utilizzo e sui modelli di business supportati, consulta *Regole di utilizzo*.

## Sviluppo di applicazioni per la riproduzione video {#develop-applications-for-video-playback}

Per consentire ai consumatori di accedere e visualizzare il contenuto, sviluppa un’applicazione di riproduzione video utilizzando Flash Player o Adobe AIR. Dopo aver sviluppato un’applicazione di riproduzione video, devi distribuirla ai consumatori. Se stai sviluppando un’applicazione utilizzando Flash Player, ospitala sul sito web della tua organizzazione. Se stai sviluppando un’applicazione utilizzando Adobe® AIR®, pubblica il programma di installazione dell’applicazione AIR in modo che i consumatori possano scaricare e installare l’applicazione sul proprio computer.

Per ulteriori informazioni sullo sviluppo di applicazioni di riproduzione video personalizzate da utilizzare con Adobe Access, vedere il capitolo &quot;Utilizzo di video&quot; in [Guida per gli sviluppatori di ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html).
