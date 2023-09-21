---
description: Queste classi descrivono il lettore multimediale e le relative risorse.
title: Classi di lettore multimediale
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Classi di lettore multimediale {#media-player-classes}

Puoi utilizzare l’API Objective-C del lettore Primetime per personalizzare il comportamento del lettore.

Queste classi descrivono il lettore multimediale e le relative risorse.

<table frame="all" colsep="1" rowsep="1" id="table_bm2_wl2_2m"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Classe</b> </td> 
   <td colname="2"><b>Descrizione</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTABRControlParameters.html" format="html" scope="external"> PTABRControlParameters</a></span> </td> 
   <td colname="2">Incapsula tutti i parametri di controllo del bit rate adattivo. I parametri supportati sono: 
    <ul id="ul_pnh_hm2_2m"> 
     <li id="li_46572FE1EB514AFF8C9F731E44DAF30B"><span class="codeph"> minBitRate</span> </li> 
     <li id="li_A10C75C9A5234241A5B84A4139F4D143"><span class="codeph"> maxBitRate</span> </li> 
     <li id="li_4E77E367A2E848D2B3E1A9C52209A7B2"><span class="codeph"> initialBitRate</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDefaultMediaPlayerClientFactory.html" format="html" scope="external"> PTDefaultMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> Implementazione predefinita di <span class="codeph"> PTMediaPlayerClientFactory</span> nel TVSDK. Fornisce i <span class="codeph"> PTOchanceResolver</span>, <span class="codeph"> PTContentResolver</span>, e <span class="codeph"> PTAdPolicySelector</span> istanze. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html" format="html" scope="external"> PTMediaPlayer</a></span> </td> 
   <td colname="2">Definisce il componente radice per il framework del lettore Primetime. <p>Le applicazioni creano un'istanza di questa classe per riprodurre un file multimediale. Questo componente invia notifiche per comunicare all’applicazione lo stato del lettore in qualsiasi momento. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTMediaPlayerClientFactory.html" format="html" scope="external"> PTMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> Protocollo che descrive i metodi che una client factory del lettore multimediale personalizzato deve implementare per fornire i <span class="codeph"> PTOchanceResolver</span> , <span class="codeph"> PTContentResolver</span> e <span class="codeph"> PTAdPolicySelector</span> istanze. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerItem.html" format="html" scope="external"> PTMediaPlayerItem</a></span> </td> 
   <td colname="2"> Rappresenta un supporto audio-video specifico. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerView.html" format="html" scope="external"> PTMediaPlayerView</a></span> </td> 
   <td colname="2"> Gestisce il componente di visualizzazione del framework del lettore Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaProfile.html" format="html" scope="external"> PTMediaProfile</a></span> </td> 
   <td colname="2"> Rappresenta il profilo di un singolo flusso nella playlist delle varianti. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaSelectionOption.html" format="html" scope="external"> PTMediaSelectionOption</a></span> </td> 
   <td colname="2">Rappresenta una risorsa di media audiovisivi per adattarsi a diverse preferenze linguistiche, requisiti di accessibilità o configurazioni di applicazioni personalizzate. Tipi di opzioni validi: 
    <ul id="ul_p2q_gn2_2m"> 
     <li id="li_46BE5AE49732481FB6D336FFF896E5AD">Sottotitoli (<span class="codeph"> PTMediaSelectionOptionTypeSubtitle</span>) </li> 
     <li id="li_6CEADCA12D4A48B7AE4A539985F32119">Audio alternativo (<span class="codeph"> PTMediaSelectionOptionTypeAudio</span>) </li> 
     <li id="li_248D3D997F8A4B6E9B48869F84060D1F"> <p>Non definito (<span class="codeph"> PTMediaSelectionOptionTypeUndefined</span>) </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTOpportunityResolver.html" format="html" scope="external"> PTOchanceResolver</a> </span> classe, <span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolver.html" format="html" scope="external"> PTOchanceResolver</a> protocollo</span> </td> 
   <td colname="2"> Classe utilizzata per l’elaborazione dei segnali nel manifesto che verranno utilizzati come posizionamenti per il processo decisionale per gli annunci di Adobe Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolverDelegate.html" format="html" scope="external"> PTOpportunityResolverDelegate</a></span> </td> 
   <td colname="2"> Protocollo che descrive i metodi di risoluzione delle opportunità personalizzate ( <span class="codeph"> PTOchanceResolver</span> ) deve utilizzare per comunicare al delegato lo stato della risoluzione dell’opportunità. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDK.html" format="html" scope="external"> PTSDK</a></span> </td> 
   <td colname="2"> Descrive la versione di TVSDK e le relative funzionalità. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDKConfig.html" format="html" scope="external"> PTSDKConfig</a></span> </td> 
   <td colname="2"> Espone le impostazioni globali di TVSDK e consente a un’applicazione di abbonarsi a tag HLS personalizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTextStyleRule.html" format="html" scope="external"> PTTextStyleRule</a></span> </td> 
   <td colname="2"> Definisce le costanti che rappresentano le chiavi di attributo di stile del testo che costituiscono il dizionario delle regole. </td> 
  </tr> 
 </tbody> 
</table>
