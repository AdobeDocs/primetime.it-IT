---
description: Potete configurare i nomi dei tag personalizzati in un flusso con la classe MediaPlayerItemConfig.
seo-description: Potete configurare i nomi dei tag personalizzati in un flusso con la classe MediaPlayerItemConfig.
seo-title: Metodi della classe di configurazione per i tag
title: Metodi della classe di configurazione per i tag
uuid: 222a0349-58d5-4bf3-9d03-e5920610faf5
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Metodi della classe di configurazione per i tag{#config-class-methods-for-tags}

Potete configurare i nomi dei tag personalizzati in un flusso con la classe MediaPlayerItemConfig.

Per creare una nuova `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

Di seguito sono riportate alcune informazioni sull&#39;utilizzo dei metodi `MediaPlayerItemConfig` per gestire i tag personalizzati:

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
   <td colname="col2"> <p>Recupera l'elenco corrente di tag sottoscritti. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Imposta l'elenco dei tag sottoscritti esposti all'applicazione. </p> <p>L'applicazione viene inoltre sottoscritta automaticamente a tutti i tag trasmessi tramite <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizzare i tag degli annunci utilizzati dal rilevatore di opportunità predefinito  </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>Recupera l'elenco corrente di tag degli annunci. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>Imposta l'elenco dei tag degli annunci da utilizzare per il generatore di opportunità predefinito. </p> </td> 
  </tr> 
 </tbody> 
</table>

Ricorda quanto segue:

* Il nome del tag personalizzato deve contenere il prefisso `#`.

   Ad esempio, `#EXT-X-ASSET` è un nome di tag personalizzato corretto, ma `EXT-X-ASSET` non è corretto.

* Non è possibile modificare la configurazione dopo il caricamento del flusso multimediale.

