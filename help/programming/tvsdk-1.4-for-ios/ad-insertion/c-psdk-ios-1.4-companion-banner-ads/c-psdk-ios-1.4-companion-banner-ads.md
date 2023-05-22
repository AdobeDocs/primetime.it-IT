---
description: TVSDK supporta gli annunci banner correlati, ovvero gli annunci che accompagnano un annuncio lineare e che spesso rimangono sulla pagina al termine dell’annuncio lineare. L'applicazione è responsabile della visualizzazione dei banner correlati forniti con un annuncio lineare.
title: Banner pubblicitari
exl-id: e7b0ce38-e4b0-4e10-8d76-2d43d8eff665
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Banner pubblicitari {#companion-banner-ads}

TVSDK supporta gli annunci banner correlati, ovvero gli annunci che accompagnano un annuncio lineare e che spesso rimangono sulla pagina al termine dell’annuncio lineare. L&#39;applicazione è responsabile della visualizzazione dei banner correlati forniti con un annuncio lineare.

Quando visualizzi gli annunci correlati, segui queste raccomandazioni:

* Tenta di presentare tutti gli annunci banner associati a un annuncio video che rientrano nel layout del lettore.
* Presentare un banner correlato solo se la posizione corrisponde esattamente all&#39;altezza e alla larghezza specificate.

   >[!TIP]
   >
   >Non ridimensionare il banner.

* Presenta il banner/i correlato/i il prima possibile dopo l’inizio dell’annuncio.
* Non sovrapporre il contenitore principale annuncio/video con i banner correlati.
* Continua a visualizzare i banner associati dopo la fine dell’annuncio.

   Lo standard prevede la visualizzazione di ogni banner complementare fino a quando non si dispone di un banner sostitutivo.

## Dati banner aziendale {#companion-banner-data}

Il contenuto di una risorsa PTA descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Il `PTMediaPlayerAdStartedNotification` la notifica restituisce un `PTAd` istanza che contiene un `companionAssets` proprietà (array di `PtAdAsset`).
Ogni `PtAdAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Informazioni disponibili </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> larghezza </td> 
   <td colname="col2"> Larghezza in pixel del banner correlato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altezza </td> 
   <td colname="col2"> Altezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Il tipo di risorsa per questo banner correlato: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: i dati sono nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: i dati sono un URL iframe (src). </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">static: i dati sono un staticURL che è un URL diretto a un’immagine. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dati </td> 
   <td colname="col2"> Dati del tipo specificato da <span class="codeph"> resourceType</span> per questo banner. </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza banner pubblicitari {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze di banner e consentire a TVSDK di ascoltare eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari correlati associati a un annuncio lineare tramite `PTMediaPlayerAdPlayStartedNotification` notifica.

I manifesti possono specificare gli annunci banner correlati in base a:

* Un frammento di HTML
* URL di una pagina iFrame
* URL di un&#39;immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, TVSDK indica i tipi disponibili per l’applicazione.

1. Creare un `PTAdBannerView`  per ogni companion ad slot sulla pagina.

       Assicurati di aver fornito le seguenti informazioni:
   
   * Per impedire il recupero di annunci correlati di dimensioni diverse, è necessario specificare un&#39;istanza del banner che specifichi la larghezza e l&#39;altezza.
   * Dimensioni banner standard.

1. Aggiungere un osservatore per `PTMediaPlayerAdStartedNotification` che effettua le seguenti operazioni:
   1. Cancella gli annunci esistenti nell’istanza del banner.
   1. Ottiene l’elenco degli annunci correlati da `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Se l’elenco degli annunci correlati non è vuoto, scorri l’elenco per le istanze del banner.

      Ogni istanza del banner ( a `PTAdAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statica) e dati necessari per visualizzare il banner correlato.
   1. Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per tale annuncio video.

      Per visualizzare un annuncio di visualizzazione autonomo, aggiungi la logica allo script per eseguire un normale tag annuncio di visualizzazione DFP (DoubleClick for Publishers) nell’istanza del banner appropriata.
   1. Invia le informazioni sul banner a una funzione sulla pagina che visualizza i banner in una posizione appropriata.

      Questo è di solito un `div`, e la tua funzione utilizza `div ID` per visualizzare il banner. Ad esempio:

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
