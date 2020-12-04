---
description: TVSDK supporta i banner pubblicitari di compagnia, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell'annuncio lineare. La vostra applicazione è responsabile della visualizzazione dei banner associati forniti con un annuncio lineare.
seo-description: TVSDK supporta i banner pubblicitari di compagnia, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell'annuncio lineare. La vostra applicazione è responsabile della visualizzazione dei banner associati forniti con un annuncio lineare.
seo-title: Annunci per banner
title: Annunci per banner
uuid: 522578ff-1f09-48f1-91f7-f074cfd34064
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# Annunci per banner completi {#companion-banner-ads}

TVSDK supporta i banner pubblicitari di compagnia, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell&#39;annuncio lineare. La vostra applicazione è responsabile della visualizzazione dei banner associati forniti con un annuncio lineare.

Quando visualizzate annunci di accompagnamento, attenetevi alle seguenti raccomandazioni:

* Tentate di presentare tutti gli annunci di banner pubblicitari associati a un video pubblicitari che si adattano al layout del vostro lettore.
* Presentate un banner complementare solo se disponete di una posizione che corrisponda esattamente a altezza e larghezza specificate.

   >[!TIP]
   >
   >Non ridimensionate il banner.

* Presentate i banner di accompagnamento il prima possibile dopo l’inizio dell’annuncio.
* Non sovrapponete il contenitore di annunci/video principale con i banner complementari.
* Continuate a visualizzare i banner complementari dopo la fine dell’annuncio.

   Lo standard prevede la visualizzazione di ciascun banner complementare fino a quando non si dispone di una sostituzione per questo banner.

## Dati del banner della compagnia {#companion-banner-data}

Il contenuto di una risorsa PTAdAsset descrive un banner complementare.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

La notifica `PTMediaPlayerAdStartedNotification` restituisce un&#39;istanza `PTAd` che contiene una proprietà `companionAssets` (array di `PtAdAsset`).
Ogni `PtAdAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Informazioni disponibili</b></th> 
   <th colname="col2" class="entry"><b>Descrizione</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Larghezza del banner di accompagnamento, in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altezza del banner ausiliario, in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Il tipo di risorsa per il banner ausiliario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: I dati si trovano nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: I dati sono un URL iframe (src). </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">static: I dati sono un URL statico che è un URL diretto a un’immagine. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> data </td> 
   <td colname="col2"> I dati del tipo specificato da <span class="codeph">resourceType</span> per il banner ausiliario. </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento di notifica `PTMediaPlayerAdPlayStartedNotification`.

I manifesti possono specificare annunci banner complementari per:

* Snippet HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobi 

Per ogni annuncio aggiuntivo complementare, TVSDK indica quali tipi sono disponibili per l’applicazione.

1. Create un&#39;istanza `PTAdBannerView` per ciascun annuncio aggiuntivo complementare sulla pagina.

       Verificate che siano state fornite le seguenti informazioni:
   
   * Per impedire il recupero di annunci companion di dimensioni diverse, un’istanza di banner che specifica la larghezza e l’altezza.
   * Dimensioni dei banner standard.

1. Aggiungete un osservatore per la `PTMediaPlayerAdStartedNotification` che esegue le seguenti operazioni:
   1. Cancella gli annunci esistenti nell&#39;istanza del banner.
   1. Ottiene l&#39;elenco degli annunci complementari da `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Se l&#39;elenco degli annunci complementari non è vuoto, ripetete l&#39;operazione sull&#39;elenco per le istanze del banner.

      Ogni istanza del banner ( a `PTAdAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner ausiliario.
   1. Se un annuncio video non contiene annunci pubblicitari associati, l’elenco delle risorse ausiliarie non contiene dati per tale annuncio video.

      Per visualizzare un annuncio di visualizzazione indipendente, aggiungete la logica allo script per eseguire un tag di annuncio di visualizzazione normale DFP (DoubleClick for Publishers) nell&#39;istanza di banner appropriata.
   1. Invia le informazioni sul banner a una funzione sulla pagina che visualizza i banner in una posizione appropriata.

      In genere si tratta di un `div` e la funzione utilizza il `div ID` per visualizzare il banner. Ad esempio:

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
