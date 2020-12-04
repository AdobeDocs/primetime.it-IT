---
seo-title: Rinnovare i certificati
title: Rinnovare i certificati
uuid: 12a560b0-966b-424e-bfe5-22e9c10d8667
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Rinnova certificati{#renew-certificates}

Devi conoscere le seguenti limitazioni per il rinnovo del certificato basate sulla configurazione dell’SDK DRM di Adobe Primetime :

* Primetime DRM Production SDK

    Adobe fornisce il set iniziale di certificati gratuiti per l&#39;SDK di produzione DRM di Primetime al momento dell&#39;acquisto di un contratto di assistenza. Se non si dispone di un contratto di assistenza, è possibile acquistare una serie di certificati di rinnovo validi per due anni.
* SDK valutazione DRM di Primetime

   Il set di certificati per questo SDK è valido per un anno e non può essere rinnovato.
* SDK di prova DRM Primetime

   L&#39;SDK di prova DRM di Primetime è valido per tre mesi e  Adobe fornisce un set di certificati di rinnovo gratuiti.

## Implementazione di nuovi certificati e utilizzo di vecchi certificati per il contenuto esistente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

In DRM di Primetime, è possibile consentire a un server licenze di rilasciare una licenza per il contenuto che viene incluso in un pacchetto con certificati del packager precedenti (o persino scaduti). Per configurare il server in modo che accetti le richieste di licenza dal contenuto precedentemente incluso nel pacchetto, fornire il vecchio certificato al server e aggiornare il file di configurazione del server in modo che il server sappia dove trovare i vecchi certificati. Per ulteriori informazioni, vedere *Gestione degli aggiornamenti dei certificati quando  certificati rilasciati dal Adobe scadono* in *Utilizzo dell&#39;SDK Adobe Primetime DRM  per la protezione dei contenuti*.

Se l&#39;applicazione server è basata sull&#39;implementazione di riferimento DRM di Primetime, non è necessario aggiornare il programma lato server. Nel file `flashaccess-refimpl.properties` sono presenti campi in cui è possibile specificare certificati Trasporto e Server licenze aggiuntivi. Se si dispone di un solo certificato, non è necessario compilare tali proprietà. Se si dispone di certificati scaduti e si desidera utilizzare tali certificati al momento del rilascio delle risposte di licenza, è necessario fornire tali certificati al file di configurazione e riavviare il server.

Per specificare vecchi certificati, utilizzare le seguenti proprietà:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

