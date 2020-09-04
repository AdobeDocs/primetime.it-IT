---
description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una cronologia.
seo-description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una cronologia.
seo-title: Classi pubblicitarie nella timeline
title: Classi pubblicitarie nella timeline
uuid: b36d128f-7f13-4c61-b925-dfa5cd94e255
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Classi pubblicitarie nella timeline{#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano all&#39;interno di una cronologia.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">Classe che definisce l'astrazione degli annunci e contiene tutte le informazioni sugli annunci. È definito da un ID univoco, una durata e un codice MediaResource. MediaResource contiene l’URL in cui risiede il contenuto effettivo dell’annuncio. 
    <pre>
      Rappresenta una risorsa lineare primaria unita al contenuto. Facoltativamente, può contenere un array di risorse ausiliarie da visualizzare insieme alla risorsa lineare.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">Classe che rappresenta una risorsa da visualizzare. 
    <pre>
      Rappresenta una risorsa da visualizzare.
    </pre> 
    <pre>
      Classe che rappresenta una risorsa annuncio.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      Visualizza una risorsa banner. L'applicazione deve creare una nuova istanza di questa classe di utilità, impostare la risorsa banner e aggiungerla a una vista. Il monitoraggio dell'impressione e del clic per il banner è gestito internamente da questa classe.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti in un determinato momento durante la riproduzione. 
    <pre>
      Rappresenta una sequenza continua di annunci associati al contenuto.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e sul titolo che è possibile utilizzare per fornire ulteriori informazioni all’utente. 
    <pre>
      Rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e sul titolo che è possibile utilizzare per fornire ulteriori informazioni all’utente.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> Protocollo che definisce le proprietà per le chiamate API AdPolicySelector. Queste proprietà forniscono il contesto per l'imposizione di ogni comportamento annuncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PTAdPolicySelector</td> 
   <td colname="2"> Un protocollo di selezione criteri per l'annuncio da applicare ai comportamenti. Le applicazioni possono essere conformi a questo protocollo implementando tutti i metodi richiesti o estendendo la classe di selezione dei criteri predefinita esistente per personalizzare comportamenti specifici. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> PTAdTimeline</td> 
   <td colname="2"> Classe che rappresenta la cronologia delle interruzioni all'interno del contenuto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> , classe <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> , protocollo
    </pre> </td> 
   <td colname="2"> Classe che gestisce la parte di risoluzione degli annunci nel processo di decisione  Adobe Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protocollo che descrive i metodi che il risolutore di contenuti personalizzato ( <span class="codeph"> PTContentResolver</span> ) deve utilizzare per comunicare al delegato lo stato della risoluzione del contenuto. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">Classe che raccoglie una richiesta di informazioni sul posizionamento. A ciascun annuncio risolto deve essere collegata una sola informazione di posizionamento. Le informazioni sulla posizione descrivono la posizione in cui l'annuncio deve essere inserito nella timeline. Contiene informazioni quali: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Posizione (in ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Tipo di posizionamento (preroll, medio o post-rollio) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Durata del blocco contenuto principale che sta per essere sostituito </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

