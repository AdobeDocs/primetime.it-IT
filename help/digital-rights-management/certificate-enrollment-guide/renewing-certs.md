---
title: Rinnova certificati
description: Rinnova certificati
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Rinnova certificati{#renew-certificates}

Tieni presente le seguenti restrizioni di rinnovo del certificato basate sulla configurazione dell’SDK DRM di Adobe Primetime:

* SDK per produzione DRM di Primetime

   Adobe fornisce l’insieme iniziale di certificati gratuiti per l’SDK di produzione DRM di Primetime quando si acquista un contratto di assistenza. Se non si dispone di un contratto di assistenza, è possibile acquistare un set di certificati di rinnovo validi per due anni.
* SDK di valutazione DRM di Primetime

   Il certificato impostato per questo SDK è valido per un anno e non può essere rinnovato.
* SDK di prova DRM di Primetime

   L’SDK di prova DRM di Primetime è valido per tre mesi e Adobe fornisce un set di certificati di rinnovo gratuiti.

## Implementazione di nuovi certificati e utilizzo di vecchi certificati per il contenuto esistente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

In DRM di Primetime, puoi consentire a un server di licenze di rilasciare una licenza per il contenuto che viene imballato con certificati del packager precedenti (o anche scaduti). Per configurare il server in modo che accetti le richieste di licenza da contenuti in pacchetti precedenti, fornisci il vecchio certificato al server e aggiorna il file di configurazione del server in modo che il server sappia dove trovare i vecchi certificati. Per ulteriori informazioni, consulta *Gestione degli aggiornamenti dei certificati quando i certificati rilasciati da un Adobe scadono* in *Utilizzo dell’SDK DRM di Adobe Primetime per la protezione dei contenuti*.

Se l&#39;applicazione server è basata sull&#39;implementazione di riferimento DRM di Primetime, non è necessario aggiornare il programma lato server. Nel file `flashaccess-refimpl.properties` sono presenti campi in cui è possibile specificare certificati Transport e License Server aggiuntivi. Se disponi di un solo certificato, non è necessario compilare tali proprietà. Se si dispone di certificati scaduti e si desidera utilizzare tali certificati quando si emettono risposte di licenza, è necessario fornire tali certificati al file di configurazione e riavviare il server.

Per specificare certificati obsoleti, utilizzare le seguenti proprietà:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

