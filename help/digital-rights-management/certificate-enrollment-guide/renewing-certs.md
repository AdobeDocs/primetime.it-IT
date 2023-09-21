---
title: Rinnovare i certificati
description: Rinnovare i certificati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Rinnovare i certificati{#renew-certificates}

Tieni presente le seguenti restrizioni per il rinnovo dei certificati basate sulla configurazione dell’SDK Adobe Primetime DRM:

* SDK di produzione DRM di Primetime

  L&#39;Adobe fornisce il set iniziale di certificati gratuiti per Primetime DRM Production SDK quando si acquista un contratto di assistenza. Se non si dispone di un contratto di assistenza, è possibile acquistare un set di certificati di rinnovo validi per due anni.
* SDK di valutazione DRM di Primetime

  Il certificato impostato per questo SDK è valido per un anno e non può essere rinnovato.
* SDK di prova di Primetime DRM

  L’SDK di prova di Primetime DRM è valido per tre mesi e Adobe fornisce un set di certificati di rinnovo gratuiti.

## Implementazione di nuovi certificati e utilizzo dei certificati precedenti per il contenuto esistente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

In DRM di Primetime è possibile consentire a un server licenze di rilasciare una licenza per il contenuto fornito con certificati Packager precedenti (o anche scaduti). Per configurare il server in modo che accetti le richieste di licenza da contenuti inclusi in un pacchetto precedente, fornisci il vecchio certificato al server e aggiorna il file di configurazione del server in modo che il server sappia dove trovare i vecchi certificati. Per ulteriori informazioni, consulta *Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi* in *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti*.

Se l&#39;applicazione server è basata sull&#39;implementazione di riferimento DRM di Primetime, non è necessario aggiornare il programma lato server. In `flashaccess-refimpl.properties` , sono disponibili campi in cui è possibile specificare ulteriori certificati di trasporto e server licenze. Se disponi di un solo certificato, non è necessario compilare tali proprietà. Se si dispone di certificati scaduti e si desidera utilizzarli quando si emettono le risposte alle licenze, è necessario fornire tali certificati al file di configurazione e riavviare il server.

Per specificare i certificati obsoleti, utilizzare le proprietà seguenti:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
