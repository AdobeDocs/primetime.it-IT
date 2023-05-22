---
description: È possibile configurare nomi di tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o basati su flusso con la classe MediaPlayerItemConfig.
title: Metodi di classe di configurazione per i tag
exl-id: 093720df-9c2d-41f1-ba9d-9553c5df40a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Metodi di classe di configurazione per i tag{#config-class-methods-for-tags}

È possibile configurare nomi di tag personalizzati in TVSDK a livello globale con la classe MediaPlayerItemConfig o basati su flusso con la classe MediaPlayerItemConfig.

TVSDK applica automaticamente la configurazione globale a qualsiasi flusso multimediale che non specifica una configurazione specifica per il flusso.

Entrambi `PSDKConfig` e `MediaPlayerItemConfig` esponi questi metodi per gestire i tag personalizzati:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> funzione pubblica get subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera l’elenco corrente dei tag seguiti. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> funzione pubblica set subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2">Imposta l'elenco dei tag sottoscritti che verranno esposti all'applicazione. <p>L’applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalizzare i tag degli annunci utilizzati dal rilevatore opportunità predefinito </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> funzione pubblica ottenere adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera l’elenco corrente dei tag annuncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> set di funzioni pubbliche adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Imposta l’elenco dei tag annuncio che verranno utilizzati dal generatore di opportunità predefinito. </td> 
  </tr> 
 </tbody> 
</table>

Tenere presente quanto segue:

* I metodi setter non consentono che il parametro tags contenga valori null.

   Se rilevato, TVSDK genera un `IllegalArgumentException`.
* Il nome del tag personalizzato deve contenere il prefisso #.

   Ad esempio: `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.
* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
