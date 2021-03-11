---
description: Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig .
title: Metodi della classe di configurazione per i tag
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag {#config-class-methods-for-tags}

Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig .

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifichi una configurazione specifica per il flusso.

`MediaPlayerItemConfig` espone questi metodi per gestire i tag personalizzati:

**Iscriviti a tag personalizzati specifici**

| <b>Metodo</b> | <b>Descrizione</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Recupera l’elenco corrente dei tag sottoscritti. |
| `public final void setSubscribedTags(String[] tags);` | Imposta l’elenco dei tag sottoscritti che verranno esposti all’applicazione.  L&#39;applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite `setAdTags`. |

**Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito**

| <b>Metodo</b> | <b>Descrizione</b> |
|--- |--- |
| `public final String[] getAdTags;` | Recupera l’elenco corrente dei tag degli annunci. |
| `public final void setAdTags(String[] tags);` | Imposta l’elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. |

Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.

   Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere il prefisso `#` .

   Ad esempio, `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.