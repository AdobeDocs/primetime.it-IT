---
description: È possibile configurare nomi di tag personalizzati in un flusso con la classe MediaPlayerItemConfig.
title: Metodi di classe di configurazione per i tag
exl-id: 864d5c35-2b26-447b-8134-414e82096f18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Metodi di classe di configurazione per i tag{#config-class-methods-for-tags}

È possibile configurare nomi di tag personalizzati in un flusso con la classe MediaPlayerItemConfig.

Per creare un nuovo `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

Di seguito sono riportate alcune informazioni su come `MediaPlayerItemConfig` I metodi vengono utilizzati per gestire i tag personalizzati:

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Iscriviti a tag personalizzati specifici</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Recupera l’elenco corrente dei tag seguiti. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Imposta l’elenco dei tag sottoscritti esposti all’applicazione. </p> <p>L’applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizzare i tag degli annunci utilizzati dal rilevatore opportunità predefinito </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>Recupera l’elenco corrente dei tag annuncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>Imposta l'elenco dei tag di annunci da utilizzare per il generatore di opportunità predefinito. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenere presente quanto segue:

* Il nome del tag personalizzato deve contenere `#` prefisso.

   Ad esempio: `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.
