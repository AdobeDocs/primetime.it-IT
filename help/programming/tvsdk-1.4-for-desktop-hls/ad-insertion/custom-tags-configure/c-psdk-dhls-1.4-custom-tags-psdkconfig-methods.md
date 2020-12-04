---
description: Potete configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o in base al flusso con la classe MediaPlayerItemConfig.
seo-description: Potete configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o in base al flusso con la classe MediaPlayerItemConfig.
seo-title: Metodi della classe di configurazione per i tag
title: Metodi della classe di configurazione per i tag
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag{#config-class-methods-for-tags}

Potete configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o in base al flusso con la classe MediaPlayerItemConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

Sia `PSDKConfig` che `MediaPlayerItemConfig` esporre questi metodi per gestire i tag personalizzati:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function get subscriptionTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Recupera l'elenco corrente di tag sottoscritti. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set subscriTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2">Imposta l'elenco dei tag sottoscritti che verranno esposti all'applicazione. <p>L'applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito  </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function get adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Recupera l'elenco corrente di tag degli annunci. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Imposta l'elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. </td> 
  </tr> 
 </tbody> 
</table>

Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.

   Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere il prefisso #.

   Ad esempio, `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.
* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.

