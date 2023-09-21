---
description: Puoi configurare nomi di tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig.
title: Metodi di classe di configurazione per i tag
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Metodi di classe di configurazione per i tag {#config-class-methods-for-tags}

Puoi configurare nomi di tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

`MediaPlayerItemConfig` espone questi metodi per gestire i tag personalizzati:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscscriptionTags </span> </td> 
   <td colname="col2"> <p>Recupera l’elenco corrente dei tag seguiti. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> void setSubscscriptionTags(String[] tags) finale pubblico; </span> </td> 
   <td colname="col2"> <p>Imposta l'elenco dei tag sottoscritti che verranno esposti all'applicazione. </p> <p>L’applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizzare i tag degli annunci utilizzati dal rilevatore opportunità predefinito</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>Recupera l’elenco corrente dei tag annuncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> void setAdTags(String[] tags) finale pubblico; </span> </td> 
   <td colname="col2"> <p>Imposta l’elenco dei tag annuncio che verranno utilizzati dal generatore di opportunità predefinito. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenere presente quanto segue:

* I metodi setter non consentono che il parametro tags contenga valori null.

  Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere `#` prefisso.

  Ad esempio: `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
