---
description: Con  Adobe Primetime DRM Server for Protected Streaming, potete specificare tutte le regole di utilizzo sul server con i file di configurazione.
seo-description: Con  Adobe Primetime DRM Server for Protected Streaming, potete specificare tutte le regole di utilizzo sul server con i file di configurazione.
seo-title: Informazioni sulle regole di utilizzo
title: Informazioni sulle regole di utilizzo
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Informazioni sulle regole di utilizzo{#about-usage-rules}

Con  Adobe Primetime DRM Server for Protected Streaming, potete specificare tutte le regole di utilizzo sul server con i file di configurazione.

Eventuali regole di utilizzo specificate nel criterio DRM per il contenuto protetto vengono sostituite.  Adobe consiglia pertanto di utilizzare un criterio DRM semplice e anonimo durante la creazione del pacchetto di contenuti. Qualsiasi regola di utilizzo che puoi configurare può essere configurata in base al tenant.

Il server DRM di Primetime per lo streaming protetto supporta le seguenti regole di utilizzo:

* Protezione dell&#39;output
*  limitazioni delle applicazioni Adobe® AIR®, SWF, iOS e Android
* Limitazioni per i moduli DRM e Runtime
* Applicazione del rilevamento Jailbreak sulle piattaforme DRM di Primetime che supportano il rilevamento Jailbreak
* La memorizzazione della cache delle licenze è disabilitata per impostazione predefinita. Memorizzazione nella cache delle licenze che è possibile attivare specificando la data di fine del caching o un periodo di tempo consentito; inizia al rilascio della licenza.
* Più diritti di riproduzione che consentono di specificare diverse combinazioni di Protezione output, Restrizioni applicazione e Limitazioni DRM/Runtime. Ad esempio, è possibile specificare diversi requisiti di protezione dell&#39;output per ogni piattaforma client utilizzando la limitazione del modulo DRM con Protezione output.

>[!NOTE]
>
>Se desiderate supportare la consegna di chiavi remote ai dispositivi iOS, il criterio DRM applicato al momento della creazione del pacchetto deve avere la consegna di chiavi remote abilitata. Questa impostazione non può essere modificata tramite la configurazione tenant sul server.

