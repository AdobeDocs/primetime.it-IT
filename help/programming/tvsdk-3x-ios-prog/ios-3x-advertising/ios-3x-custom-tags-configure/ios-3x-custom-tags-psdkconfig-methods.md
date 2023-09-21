---
description: È possibile configurare nomi di tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig.
title: Metodi di classe di configurazione per i tag
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Metodi di classe di configurazione per i tag {#config-class-methods-for-tags}

È possibile configurare nomi di tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

`PTSDKConfig` espone questi metodi per gestire i tag personalizzati:

| **Iscriviti a tag personalizzati specifici** |  |
|---|---|
| `subscribedTags` | Recupera l’elenco corrente dei tag seguiti. |
| `setSubscribedTags` | Imposta l&#39;elenco dei tag sottoscritti che verranno esposti all&#39;applicazione. |
| **Personalizzare i tag degli annunci utilizzati dal rilevatore opportunità predefinito** |
| `adTags` | Recupera l’elenco corrente dei tag annuncio. |
| `setAdTags` | Imposta l’elenco dei tag annuncio che verranno utilizzati dal generatore di opportunità predefinito. |


Tenere presente quanto segue:

* I metodi setter non consentono che il parametro tags contenga valori null.
* Il nome del tag personalizzato deve contenere il prefisso #.

  Ad esempio, #EXT-X-ASSET è un nome di tag personalizzato corretto, ma EXT-X-ASSET non è corretto.
* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
