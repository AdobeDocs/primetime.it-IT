---
description: Puoi configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o in base al flusso con la classe MediaPlayerItemConfig.
title: Metodi della classe di configurazione per i tag
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag{#config-class-methods-for-tags}

Puoi configurare i nomi dei tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o in base al flusso con la classe MediaPlayerItemConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifichi una configurazione specifica per il flusso.

Per gestire i tag personalizzati, sia `PSDKConfig` che `MediaPlayerItemConfig` espongono questi metodi:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> funzione pubblica get subscriTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Recupera l’elenco corrente dei tag sottoscritti. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> set di funzioni pubbliche subscriptionTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2">Imposta l’elenco dei tag sottoscritti che verranno esposti all’applicazione. <p>L'applicazione viene inoltre abbonata automaticamente a tutti i tag trasmessi tramite <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito  </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> funzione pubblica get adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Recupera l’elenco corrente dei tag degli annunci. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> funzione pubblica set adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Imposta l’elenco dei tag degli annunci che verranno utilizzati dal generatore di opportunità predefinito. </td> 
  </tr> 
 </tbody> 
</table>

Ricorda quanto segue:

* I metodi setter non consentono al parametro tags di contenere valori null.

   Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere il prefisso #.

   Ad esempio, `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.
* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.

