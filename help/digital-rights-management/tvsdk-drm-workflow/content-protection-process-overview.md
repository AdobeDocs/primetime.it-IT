---
title: Panoramica del processo di acquisizione delle licenze
description: Panoramica del processo di acquisizione delle licenze
copied-description: true
exl-id: 0e1c43a5-9a7d-4534-acd6-7feff94f4670
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Panoramica del processo di acquisizione delle licenze{#license-acquisition-process-overview}

Nelle sezioni seguenti è descritto come consentire all’applicazione di riprodurre contenuti protetti da Primetime DRM, utilizzando gli esempi di codice ActionScript 3 (AS3). Le divergenze sfumate da questo flusso di lavoro per le app native su piattaforme mobili vengono presentate dove appropriato. Tuttavia, i flussi di lavoro DRM di Primetime sono molto simili in tutte le piattaforme, pertanto la tua comprensione del codice AS3 renderà l’estrapolazione ad altre piattaforme abbastanza semplice.

**Processo di acquisizione licenza:**

1. Ottenere i metadati DRM del contenuto protetto.
1. Verifica se una licenza è disponibile localmente:

   * Se la licenza è disponibile localmente, caricarla e passare al punto 6.
   * Se la licenza non è disponibile localmente, procedere al passaggio 3.

1. Controlla se è richiesta l’autenticazione:

   * Se è richiesta l&#39;autenticazione, ottenere le credenziali di autenticazione dall&#39;utente e passarle al server licenze.
   * Se non è richiesta l’autenticazione, passa al passaggio 6.

1. Se è richiesta la registrazione del dominio del dispositivo, aggiungi il dominio del dispositivo.
1. Se l&#39;autenticazione era necessaria e ora è completa, scaricare la licenza dal server licenze.
1. Riproduci il contenuto.

Se non si sono verificati errori e l’utente è stato autorizzato a visualizzare il contenuto, Primetime invia una `DRMStatusEvent` e l&#39;applicazione inizia la riproduzione. Il `DRMStatusEvent` L&#39;oggetto contiene le informazioni sulla licenza correlate, che identificano i criteri e le autorizzazioni dell&#39;utente. Ad esempio: `DRMStatusEvent` può contenere informazioni relative alla possibilità di rendere il contenuto disponibile offline, alla scadenza della licenza e così via.

L’applicazione può utilizzare le informazioni sulla licenza per informare l’utente dello stato del proprio criterio. Ad esempio, l’applicazione può visualizzare il numero di giorni rimanenti di cui l’utente dispone per visualizzare il contenuto su una barra di stato. Se all’utente è consentito l’accesso offline, la licenza viene memorizzata nella cache e il contenuto crittografato viene scaricato nel computer dell’utente. Il contenuto viene reso accessibile per la durata definita nella durata di memorizzazione nella cache della licenza. La proprietà detail nell’evento contiene `DRM.voucherObtained`. L’applicazione decide dove archiviare il contenuto localmente in modo che sia disponibile offline. È inoltre possibile precaricare le licenze utilizzando `DRMManager` classe.
