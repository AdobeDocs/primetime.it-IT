---
description: Puoi configurare nomi di tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig.
title: Metodi di classe di configurazione per i tag
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Metodi di classe di configurazione per i tag {#config-class-methods-for-tags}

Puoi configurare nomi di tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

`MediaPlayerItemConfig` espone questi metodi per gestire i tag personalizzati:

**Iscriviti a tag personalizzati specifici**

| <b>Metodo</b> | <b>Descrizione</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Recupera l’elenco corrente dei tag seguiti. |
| `public final void setSubscribedTags(String[] tags);` | Imposta l&#39;elenco dei tag sottoscritti che verranno esposti all&#39;applicazione.  L’applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite `setAdTags`. |

**Personalizzare i tag degli annunci utilizzati dal rilevatore opportunità predefinito**

| <b>Metodo</b> | <b>Descrizione</b> |
|--- |--- |
| `public final String[] getAdTags;` | Recupera l’elenco corrente dei tag annuncio. |
| `public final void setAdTags(String[] tags);` | Imposta l’elenco dei tag annuncio che verranno utilizzati dal generatore di opportunità predefinito. |

Tenere presente quanto segue:

* I metodi setter non consentono che il parametro tags contenga valori null.

  Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere `#` prefisso.

  Ad esempio: `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
