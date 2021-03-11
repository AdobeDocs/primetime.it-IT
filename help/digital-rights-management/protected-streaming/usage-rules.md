---
description: Con Adobe Primetime DRM Server for Protected Streaming, puoi specificare tutte le regole di utilizzo sul server con file di configurazione.
title: Informazioni sulle regole di utilizzo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Informazioni sulle regole di utilizzo{#about-usage-rules}

Con Adobe Primetime DRM Server for Protected Streaming, puoi specificare tutte le regole di utilizzo sul server con file di configurazione.

Eventuali regole di utilizzo specificate nel criterio DRM per il contenuto protetto vengono ignorate. Pertanto, l’Adobe consiglia di utilizzare una politica DRM semplice e anonima durante la creazione dei contenuti. Tutte le regole di utilizzo configurabili possono essere configurate in base al tenant.

Il server DRM di Primetime per lo streaming protetto supporta le seguenti regole di utilizzo:

* Protezione dell&#39;uscita
* Restrizioni per applicazioni Adobe® AIR®, SWF, iOS e Android
* Restrizioni al modulo DRM e runtime
* Applicazione del rilevamento Jailbreak sulle piattaforme DRM Primetime che supportano il rilevamento jailbreak
* Il caching delle licenze è disattivato per impostazione predefinita. Memorizzazione in cache delle licenze che è possibile abilitare specificando la data di fine del caching o un periodo di tempo di memorizzazione in cache consentito; inizia al momento del rilascio della licenza.
* Diritti di riproduzione multipli che consentono di specificare diverse combinazioni di Protezione output, Restrizioni applicazione e Restrizioni DRM/Runtime. Ad esempio, è possibile specificare diversi requisiti di protezione dell&#39;output per ciascuna piattaforma client utilizzando la limitazione del modulo DRM con protezione dell&#39;output.

>[!NOTE]
>
>Se desideri supportare la consegna di chiavi remote ai dispositivi iOS, la politica DRM applicata al momento della creazione del pacchetto deve avere la consegna di chiavi remote abilitata. Impossibile modificare questa impostazione tramite la configurazione tenant sul server.

