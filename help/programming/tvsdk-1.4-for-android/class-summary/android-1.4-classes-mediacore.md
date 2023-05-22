---
description: Puoi utilizzare l’API del lettore Primetime per personalizzare il comportamento del lettore.
title: Classi Mediacore
exl-id: fdbe9cd3-a5ca-4935-b9b3-8a6c04aed9ab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Classi Mediacore {#mediacore-classes}

Puoi utilizzare l’API del lettore Primetime per personalizzare il comportamento del lettore.

Per consultare la documentazione API completa per TVSDK, vai al [Riferimenti API di Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

Queste classi descrivono il lettore multimediale e le relative risorse.
Pacchetto [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>Nome </p> </th> 
   <th colname="2" class="entry"> <p>Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParameters</a>  ABRControlParameters</span> </td> 
   <td colname="2"> Classe che incapsula tutti i parametri di controllo del bit rate adattivo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdClientFactory.html" format="html" scope="external"> AdClientFactory</a> </span> </td> 
   <td colname="2"> Interfaccia per la creazione di rilevatori di opportunità. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdvertisingFactory.html" format="html" scope="external"> AdvertisingFactory</a> </span> </td> 
   <td colname="2"> Classe factory che consente la personalizzazione del processo di ad decisioning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> ParametriControlloBuffer</a> </span> </td> 
   <td colname="2"> Classe che incapsula tutti i parametri di controllo del buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> Implementazione predefinita per i comportamenti di riproduzione degli annunci. Interfaccia che consente alle applicazioni di personalizzare i comportamenti degli annunci.</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2">Implementazione classe predefinita di <span class="codeph"> MediaPlayer</span> di rete. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a> </span> </td> 
   <td colname="2">Interfaccia pubblica per <span class="codeph"> DefaultMediaPlayer</span> classe. Include enumerazioni per Event, PlayerState e Visibility. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html" format="html" scope="external"> MediaPlayer.AdPlaybackEventListener</a></span> </td> 
   <td colname="2"> Definizione dell’interfaccia di un set di callback da richiamare durante la riproduzione dell’annuncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html" format="html" scope="external"> MediaPlayer.DRMEventListener</a></span> </td> 
   <td colname="2"> Definizione dell’interfaccia di un callback da richiamare quando diventano disponibili metadati protetti. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.EventListener.html" format="html" scope="external"> MediaPlayer.EventListener</a> </span> </td> 
   <td colname="2"> Interfaccia indicatore utilizzata per unificare la registrazione del listener di eventi. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html" format="html" scope="external"> MediaPlayer.PlaybackEventListener</a> </span> </td>
   <td colname="2"> Definizione dell’interfaccia di un set di callback da richiamare durante la riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html" format="html" scope="external"> MediaPlayer.QOSEventListener</a> </span> </td> 
   <td colname="2"> Definizione dell'interfaccia di un set di callback da richiamare durante QoS. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a> </span> </td> 
   <td colname="2"> Interfaccia che rappresenta i file multimediali audio e video. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a> </span> </td> 
   <td colname="2"> Classe che carica una risorsa del lettore multimediale e crea l'oggetto MediaPlayerItem corrispondente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html" format="html" scope="external"> MediaPlayerItemLoader.LoaderListener</a> </span> </td> 
   <td colname="2"> Interfaccia che definisce i metodi listener associati all'oggetto MediaPlayerItemLoader. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a> </span> </td> 
   <td colname="2"> Classe per la visualizzazione che verrà utilizzata da MediaPlayer per il rendering video. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a> </span> </td> 
   <td colname="2"> Classe che racchiude tutte le informazioni su una risorsa multimediale. Include l’enumerazione per il tipo di risorsa multimediale. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PlacementOpportunityDetector.html" format="html" scope="external"> RilevatoreOpportunitàPosizionamento</a> </span> </td> 
   <td colname="2"> Interfaccia utilizzata per l’elaborazione di suggerimenti nel manifesto che verranno utilizzati come posizionamenti per il processo di ad decisioning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a> </span> </td> 
   <td colname="2"> Classe che incapsula i tag personalizzati utilizzati dal lettore multimediale durante l’esecuzione del posizionamento dell’annuncio, oltre ai tag di cue predefiniti. Include inoltre i nomi dei tag di cui l’applicazione desidera ricevere notifica. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> FormatoTesto</a> </span> </td> 
   <td colname="2"> Interfaccia che racchiude diversi attributi che descrivono uno stile di testo (ad esempio, lo stile sottotitoli). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormatBuilder.html" format="html" scope="external"> TextFormatBuilder</a></span> </td> 
   <td colname="2"> Metodi di classe per impostare la formattazione del testo. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> Versione</a></span> </td> 
   <td colname="2"> Classe che fornisce la versione e la descrizione TVSDK. </td> 
  </tr> 
 </tbody> 
</table>
