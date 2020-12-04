---
seo-title: Panoramica del processo di acquisizione della licenza
title: Panoramica del processo di acquisizione della licenza
uuid: c2eedd0a-3e3a-4c2f-a781-855f0ba65b15
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Panoramica del processo di acquisizione della licenza{#license-acquisition-process-overview}

L&#39;abilitazione dell&#39;applicazione per la riproduzione di contenuto sotto la protezione di DRM di Primetime è descritta nelle sezioni seguenti, utilizzando  ActionScript 3 (AS3) esempi di codice. Se necessario, vengono presentate le partenze sfumate da questo flusso di lavoro per le app native sulle piattaforme mobili. I flussi di lavoro DRM di Primetime sono molto simili tra tutte le piattaforme, pertanto la comprensione del codice AS3 renderà l&#39;estrapolazione ad altre piattaforme abbastanza semplice.

**Processo di acquisizione della licenza:**

1. Ottenete i metadati DRM del contenuto protetto.
1. Verificate la disponibilità locale di una licenza:

   * Se la licenza è disponibile localmente, caricate la licenza e andate al punto 6.
   * Se la licenza non è disponibile localmente, procedere al punto 3.

1. Verificate che l&#39;autenticazione sia necessaria:

   * Se l&#39;autenticazione è necessaria, ottenete le credenziali di autenticazione dall&#39;utente e passatele al server delle licenze.
   * Se l&#39;autenticazione non è necessaria, andate al punto 6.

1. Se è richiesta la registrazione del dominio del dispositivo, iscriviti al dominio del dispositivo.
1. Se l&#39;autenticazione era necessaria e ora è completa, scaricate la licenza dal server licenze.
1. Riproduci il contenuto.

Se non si sono verificati errori e l&#39;utente è stato autorizzato a visualizzare il contenuto, Primetime invia un oggetto `DRMStatusEvent` e l&#39;applicazione inizia la riproduzione. L&#39;oggetto `DRMStatusEvent` contiene le relative informazioni sulla licenza, che identificano i criteri e le autorizzazioni dell&#39;utente. Ad esempio, `DRMStatusEvent` potrebbe contenere informazioni relative alla possibilità di rendere disponibile il contenuto offline, alla scadenza della licenza e così via.

L&#39;applicazione può utilizzare le informazioni sulla licenza per informare l&#39;utente dello stato dei propri criteri. Ad esempio, l&#39;applicazione può visualizzare il numero di giorni rimanenti di cui dispone l&#39;utente per visualizzare il contenuto in una barra di stato. Se all&#39;utente è consentito l&#39;accesso offline, la licenza viene memorizzata nella cache e il contenuto crittografato viene scaricato nel computer dell&#39;utente. Il contenuto è reso accessibile per la durata definita nella durata del caching delle licenze. La proprietà detail dell&#39;evento contiene `DRM.voucherObtained`. L&#39;applicazione decide dove archiviare localmente il contenuto per renderlo disponibile offline. È inoltre possibile precaricare le licenze utilizzando la classe `DRMManager`.
