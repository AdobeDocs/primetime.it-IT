---
description: Queste classi forniscono informazioni sugli annunci che si verificano in una timeline.
title: Classi di pubblicità Timeline
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Classi di pubblicità Timeline {#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano in una timeline.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Nome</b></th> 
   <th colname="2" class="entry"><b>Descrizione</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">Classe che definisce l’astrazione dell’annuncio e contiene tutte le informazioni sull’annuncio. È definito da un ID univoco, una durata e un MediaResource. MediaResource contiene l’URL in cui risiede il contenuto effettivo dell’annuncio. 
    <pre>
      Rappresenta una risorsa lineare primaria unita al contenuto. Facoltativamente, può contenere una matrice di risorse correlate che devono essere visualizzate insieme alla risorsa lineare.
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
      Visualizza una risorsa banner. L'applicazione deve creare una nuova istanza di questa classe di utilità, impostare la risorsa del banner e aggiungerla a una vista. Questa classe gestisce internamente il tracciamento delle impression e dei clic per il banner.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti ad un certo punto durante la riproduzione. 
    <pre>
      Rappresenta una sequenza continua di annunci uniti nel contenuto.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e il titolo che può essere utilizzato per fornire ulteriori informazioni all’utente. 
    <pre>
      Rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e il titolo che può essere utilizzato per fornire ulteriori informazioni all’utente.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> Protocollo che definisce le proprietà per le chiamate API AdPolicySelector. Queste proprietà forniscono il contesto per applicare ogni comportamento pubblicitario. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> Protocollo di selezione dei criteri degli annunci per l’applicazione dei comportamenti degli annunci. Le applicazioni possono conformarsi a questo protocollo implementando tutti i metodi richiesti o estendendo la classe del selettore dei criteri predefinita esistente per personalizzare comportamenti specifici. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> Classe che rappresenta la sequenza temporale delle interruzioni all'interno del contenuto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> classe, 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> protocollo
    </pre> </td> 
   <td colname="2"> Classe che gestisce la parte di risoluzione degli annunci nel processo decisionale per gli annunci di Adobe Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protocollo che descrive i metodi di risoluzione dei contenuti personalizzati ( <span class="codeph"> PTContentResolver</span> ) deve utilizzare per comunicare al delegato lo stato della risoluzione dei contenuti. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">Classe che astrae una richiesta di informazioni sul posizionamento. A ogni annuncio risolto devono essere associate una informazione di posizionamento. Le informazioni sul posizionamento descrivono dove l’annuncio deve essere inserito nella timeline. Contiene informazioni quali: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Posizione posizionamento (in ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Tipo di posizionamento (pre-roll, mid-roll o post-roll) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Durata del blocco di contenuto principale che sta per essere sostituito </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
