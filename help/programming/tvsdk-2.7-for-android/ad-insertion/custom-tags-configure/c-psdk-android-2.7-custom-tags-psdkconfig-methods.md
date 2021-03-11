---
description: Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig .
title: Metodi della classe di configurazione per i tag
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag {#config-class-methods-for-tags}

Puoi configurare globalmente i nomi dei tag personalizzati in TVSDK con la classe MediaPlayerItemConfig .

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifichi una configurazione specifica per il flusso.

`MediaPlayerItemConfig` espone questi metodi per gestire i tag personalizzati:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags  </span> </td> 
   <td colname="col2"> <p>Recupera l’elenco corrente dei tag sottoscritti. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags);  </span> </td> 
   <td colname="col2"> <p>Imposta l’elenco dei tag sottoscritti che verranno esposti all’applicazione. </p> <p>L'applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags;  </span> </td> 
   <td colname="col2"> <p>Recupera l’elenco corrente dei tag degli annunci. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags);  </span> </td> 
   <td colname="col2"> <p>Imposta l’elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. </p> </td> 
  </tr> 
 </tbody> 
</table>

Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.

   Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere il prefisso `#` .

   Ad esempio, `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
