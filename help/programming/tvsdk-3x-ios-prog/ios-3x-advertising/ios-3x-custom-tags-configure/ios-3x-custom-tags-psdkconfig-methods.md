---
description: Puoi configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig .
title: Metodi della classe di configurazione per i tag
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag {#config-class-methods-for-tags}

Puoi configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig .

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifichi una configurazione specifica per il flusso.

`PTSDKConfig` espone questi metodi per gestire i tag personalizzati:

| **Iscriviti a tag personalizzati specifici** |  |
|---|---|
| `subscribedTags` | Recupera l’elenco corrente dei tag sottoscritti. |
| `setSubscribedTags` | Imposta l’elenco dei tag sottoscritti che verranno esposti all’applicazione. |
| **Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito** |
| `adTags` | Recupera l’elenco corrente dei tag degli annunci. |
| `setAdTags` | Imposta l’elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. |


Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.
* Il nome del tag personalizzato deve contenere il prefisso #.

   Ad esempio, #EXT-X-ASSET è un nome di tag personalizzato corretto, ma EXT-X-ASSET non è corretto.
* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.