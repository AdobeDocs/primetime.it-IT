---
description: Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig.
seo-description: Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig.
seo-title: Metodi della classe di configurazione per i tag
title: Metodi della classe di configurazione per i tag
uuid: 64284876-1f31-47e0-a99b-3bfe17e10707
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Metodi della classe di configurazione per i tag {#config-class-methods-for-tags}

Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

`MediaPlayerItemConfig` espone questi metodi per gestire i tag personalizzati:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>Recupera l'elenco corrente di tag sottoscritti. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>Imposta l'elenco dei tag sottoscritti che verranno esposti all'applicazione. </p> <p>L’applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>Recupera l'elenco corrente di tag degli annunci. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>Imposta l'elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. </p> </td> 
  </tr> 
 </tbody> 
</table>

Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.

   Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere il `#` prefisso .

   Ad esempio, `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
