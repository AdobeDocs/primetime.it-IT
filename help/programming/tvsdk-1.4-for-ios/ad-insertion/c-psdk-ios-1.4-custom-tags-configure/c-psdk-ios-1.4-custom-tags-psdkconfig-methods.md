---
description: Potete configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig.
seo-description: Potete configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig.
seo-title: Metodi della classe di configurazione per i tag
title: Metodi della classe di configurazione per i tag
uuid: 1d3651a0-3b70-4d3a-8ced-663a9dad7205
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag{#config-class-methods-for-tags}

Potete configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe PTSDKConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

`PTSDKConfig` espone questi metodi per gestire i tag personalizzati:

| **Iscriviti a tag personalizzati specifici** |
|---|
| `subscribedTags` | Recupera l&#39;elenco corrente di tag sottoscritti. |
| `setSubscribedTags` | Imposta l&#39;elenco dei tag sottoscritti che verranno esposti all&#39;applicazione. |
| **Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito** |
| `adTags` | Recupera l&#39;elenco corrente di tag degli annunci. |
| `setAdTags` | Imposta l&#39;elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. |

Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.
* Il nome del tag personalizzato deve contenere il prefisso #.

   Ad esempio, #EXT-X-ASSET è un nome di tag personalizzato corretto, ma EXT-X-ASSET non è corretto.
* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.

