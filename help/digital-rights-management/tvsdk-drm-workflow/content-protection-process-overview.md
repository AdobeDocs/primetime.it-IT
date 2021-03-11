---
title: Panoramica del processo di acquisizione della licenza
description: Panoramica del processo di acquisizione della licenza
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Panoramica del processo di acquisizione della licenza{#license-acquisition-process-overview}

L’abilitazione dell’applicazione per riprodurre contenuti sotto la protezione di DRM di Primetime è descritta nelle sezioni seguenti, utilizzando gli esempi di codice di ActionScript 3 (AS3). Se appropriato, vengono presentate le partenze sfumate da questo flusso di lavoro per le app native sulle piattaforme mobili. I flussi di lavoro DRM di Primetime sono molto simili per tutte le piattaforme, tuttavia, la tua comprensione del codice AS3 renderà l&#39;estrapolazione ad altre piattaforme abbastanza semplice.

**Processo di acquisizione della licenza:**

1. Ottieni i metadati DRM del contenuto protetto.
1. Controlla se una licenza è disponibile localmente:

   * Se la licenza è disponibile localmente, carica la licenza e vai al passaggio 6.
   * Se la licenza non è disponibile localmente, procedere al passaggio 3.

1. Controlla se l&#39;autenticazione è necessaria:

   * Se è necessaria l’autenticazione, ottieni le credenziali di autenticazione dall’utente e trasmettili al server licenze.
   * Se l&#39;autenticazione non è necessaria, vai al passaggio 6.

1. Se è richiesta la registrazione al dominio del dispositivo, unisciti al dominio del dispositivo.
1. Se l’autenticazione era necessaria e ora è completa, scarica la licenza dal server licenze.
1. Riproduci il contenuto.

Se non si sono verificati errori e l’utente è stato autorizzato a visualizzare il contenuto, Primetime invia un oggetto `DRMStatusEvent` e l’applicazione inizia la riproduzione. L&#39;oggetto `DRMStatusEvent` contiene le relative informazioni sulla licenza, che identificano i criteri e le autorizzazioni dell&#39;utente. Ad esempio, `DRMStatusEvent` potrebbe contenere informazioni relative alla possibilità di rendere disponibile il contenuto offline, alla scadenza della licenza e così via.

L&#39;applicazione può utilizzare le informazioni sulla licenza per informare l&#39;utente dello stato dei propri criteri. Ad esempio, l’applicazione può visualizzare il numero di giorni rimanenti per la visualizzazione del contenuto in una barra di stato. Se all&#39;utente è consentito l&#39;accesso offline, la licenza viene memorizzata nella cache e il contenuto crittografato viene scaricato nel computer dell&#39;utente. Il contenuto viene reso accessibile per la durata definita nella durata del caching delle licenze. La proprietà detail nell&#39;evento contiene `DRM.voucherObtained`. L’applicazione decide dove archiviare il contenuto localmente per renderlo disponibile offline. Puoi anche precaricare le licenze utilizzando la classe `DRMManager` .
