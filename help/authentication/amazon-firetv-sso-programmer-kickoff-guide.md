---
title: Amazon fireTV SSO - Guida introduttiva al programmatore
description: Amazon fireTV SSO - Guida introduttiva al programmatore
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Amazon fireTV SSO - Guida introduttiva al programmatore {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#intro}

Questo documento descrive le informazioni necessarie per integrare il nuovo **SDK FireTV dell&#39;autenticazione Adobe Primetime** nell&#39;applicazione fireTV. Questo nuovo SDK sfrutta l&#39;integrazione a livello di sistema operativo sulla piattaforma Amazon FireTV, offrendo così **Single Sign On** supporto. Per beneficiare del Single Sign On è necessario un piccolo sforzo da parte tua per migrare l&#39;applicazione dall&#39;API Clientless al nuovo SDK di FireTV. Alcuni cambiamenti nei flussi di autenticazione saranno descritti di seguito.

## Architettura di alto livello e integrazione a livello di sistema operativo {#high}

Per ottenere il Single Sign On tra le applicazioni TV Everywhere sulla piattaforma Amazon fireTV e per migliorare l&#39;esperienza complessiva su questa piattaforma abbiamo deciso di integrare il nostro SDK principale a livello di sistema operativo fireTV. I programmatori saranno tenuti a compilare in base a una libreria di stub fornita dall&#39;Adobe. La funzionalità effettiva sarà fornita dalla libreria Adobe presente in Amazon FireTV OS.

Finché Amazon non fornirà un simulatore FireTV che incorpora la nostra libreria a livello di sistema operativo lo sviluppo sarebbe possibile solo utilizzando dispositivi FireTV reali.

## Vantaggi {#bene}

* Single Sign On tra tutte le applicazioni TV a Adobe ovunque sulla piattaforma Amazon FireTV con tutti gli MVPD integrati.
* Possibilità di usufruire di HBA (con MVPD supportati).
* Possibilità di utilizzare l&#39;SDK FireTV più recente senza dover aggiornare le applicazioni ogni volta che viene rilasciata una nuova versione SDK.
* Tutte le app TVE beneficiano dell&#39;utilizzo della libreria di sistema condivisa rimuovendo la necessità di disporre di una copia locale della libreria AccessEnabler. In questo modo si assicura anche che tutte le applicazioni utilizzino la stessa versione SDK.
* Autenticazione a schermo singolo: non è necessario il codice di registrazione e i flussi di lavoro a schermo singolo.

## Migrazione dall’app basata su API Clientless all’app basata su SDK FireTV {#migra1}

Per migrare dall’API Clientless all’SDK di FireTV è necessario rimuovere la base di codice relativa all’API Clientless e integrare il nuovo SDK di FireTV.

Rispetto all&#39;app basata su Clientless API, con il nuovo fireTV SDK l&#39;autenticazione si sposta al primo schermo, non è più necessario un&#39;autenticazione a seconda schermata.

Questo richiede ai programmatori di aggiungere un selettore MVPD nelle loro app in modo che gli utenti possano scegliere il proprio fornitore TV proprio sul dispositivo FireTV. Dopo aver selezionato MVPD, all&#39;utente verrà mostrata la pagina di accesso MVPD sul dispositivo fireTV.

I wireframe dei flussi utente che descrivono gli scenari regolari, HBA e SSO su fireTV sono disponibili in [Amazon Fire TV - Flusso utente dell&#39;accesso MVPD](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## Migrazione dall’app basata su Android SDK all’app basata su fireTV SDK {#migra2}

Questo nuovo SDK FireTV è molto simile al nostro SDK Android esistente e alla documentazione corrente disponibile per **integrazione del nostro SDK per Android** <!--http://tve.helpdocsonline.com/android-technical-overview-->può essere utilizzato finché non sono pronti i documenti dell&#39;SDK di fireTV. Se hai già applicazioni Android che utilizzano il nostro SDK per Android, l&#39;integrazione di fireTV SDK nella tua applicazione fireTV dovrebbe essere semplice.

Rispetto all&#39;SDK Android esistente, su fireTV SDK il processo di autenticazione sarà più semplice da sviluppare, poiché le attività di gestione / presentazione della pagina di accesso MVPD e il recupero del token AuthN saranno eseguite internamente dalla libreria AccessEnabler.

## Domande frequenti {#faq}

1. In che modo **SSO** lavoro?

   * SSO funzionerà su tutte le applicazioni Programmer alimentate dall&#39;autenticazione Adobe Primetime che utilizzano il nuovo SDK FireTV sullo stesso dispositivo Amazon fireTV
   * SSO tra le app Programmer implementate su Clientless REST API e le app implementate su fireTV SDK **NON sarà supportato**

1. Qual è la copertura MVPD di FireTV SSO?

   * **Tutti gli MVPD** integrato dall&#39;autenticazione Adobe Primetime sarà tecnicamente supportato dall&#39;SSO su fireTV SDK.

1. Oltre a usare il nuovo SDK, quali altri **modifiche al flusso di lavoro** I programmatori dovrebbero essere a conoscenza di?

   * I programmatori devono implementare un selettore MVPD per la piattaforma FireTV.

1. Verrà apportata una modifica all&#39;autenticazione? **TTL**?

   * Non vi è alcuna modifica nel comportamento per quanto riguarda i TTL di autenticazione.
   * Il primo token di autenticazione valido verrà utilizzato per l&#39;esecuzione dell&#39;SSO e in questo caso tutte le altre applicazioni che saranno autenticate tramite SSO utilizzeranno lo stesso TTL fino alla scadenza. Quindi, quando si passa da un&#39;applicazione all&#39;altra, la seconda applicazione condividerà il TTL della prima applicazione che esegue l&#39;autenticazione.

1. Come funziona **API di degradazione** lavoro?

   * Non sono necessarie modifiche per l’API di degradazione, l’esperienza utente sarà la stessa dei dispositivi Android.

1. Come **TempPass** i flussi sono interessati?

   * I flussi TempPass sono a schermo singolo e si comportano come su qualsiasi altro dispositivo nativo.

1. Altre funzionalità di Adobe funzioneranno come prima?

   * Tutte le funzionalità di autenticazione Primetime funzioneranno su fireTV come su dispositivi Android.
