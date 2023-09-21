---
description: Con Adobe Primetime DRM Server for Protected Streaming è possibile specificare tutte le regole di utilizzo sul server con i file di configurazione.
title: Informazioni sulle regole di utilizzo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Informazioni sulle regole di utilizzo{#about-usage-rules}

Con Adobe Primetime DRM Server for Protected Streaming è possibile specificare tutte le regole di utilizzo sul server con i file di configurazione.

Eventuali regole di utilizzo specificate nei criteri DRM per il contenuto protetto vengono ignorate. L&#39;Adobe consiglia pertanto di utilizzare una policy DRM semplice e anonima durante la creazione del pacchetto di contenuti. Tutte le regole di utilizzo che puoi configurare possono essere configurate in base al singolo tenant.

Il server DRM Primetime per Streaming protetto supporta le seguenti regole di utilizzo:

* Protezione dell&#39;output
* Limitazioni per le applicazioni Adobe® AIR®, SWF, iOS e Android
* Restrizioni per i moduli DRM e runtime
* Applicazione del rilevamento jailbreak sulle piattaforme DRM Primetime che supportano il rilevamento jailbreak
* Il caching delle licenze è disattivato per impostazione predefinita. Il caching delle licenze che è possibile abilitare specificando la data di fine del caching o la quantità di tempo consentita per il caching viene avviato al momento dell’emissione della licenza.
* Più diritti di riproduzione che consentono di specificare diverse combinazioni di protezione dell&#39;output, restrizioni dell&#39;applicazione e restrizioni DRM/runtime. Ad esempio, è possibile specificare requisiti di protezione dell&#39;output diversi per ogni piattaforma client utilizzando la limitazione del modulo DRM con protezione dell&#39;output.

>[!NOTE]
>
>Se si desidera supportare la consegna di chiavi remote ai dispositivi iOS, la consegna di chiavi remote deve essere abilitata per i criteri DRM applicati al momento della creazione del pacchetto. Questa impostazione non può essere modificata tramite la configurazione tenant sul server.
