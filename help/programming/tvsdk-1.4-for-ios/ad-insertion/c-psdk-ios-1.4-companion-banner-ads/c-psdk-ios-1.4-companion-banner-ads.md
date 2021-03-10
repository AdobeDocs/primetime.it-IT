---
description: TVSDK supporta annunci per banner complementari, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell’annuncio lineare. La tua applicazione è responsabile della visualizzazione dei banner complementari che sono forniti con un annuncio lineare.
title: Annunci banner
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Annunci per banner pubblicitari {#companion-banner-ads}

TVSDK supporta annunci per banner complementari, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell’annuncio lineare. La tua applicazione è responsabile della visualizzazione dei banner complementari che sono forniti con un annuncio lineare.

Quando si visualizzano gli annunci companion, attenersi alle seguenti raccomandazioni:

* Tenta di presentare il numero di annunci banner di un annuncio video come si adatterà al layout del tuo giocatore.
* Presentare un banner complementare solo se si dispone di una posizione che corrisponde esattamente alla sua altezza e larghezza specificate.

   >[!TIP]
   >
   >Non ridimensionare il banner.

* Presenta i banner associati il prima possibile dopo l’inizio dell’annuncio.
* Non sovrapporre il contenitore principale annuncio/video con banner complementari.
* Continua a visualizzare i banner complementari dopo la fine dell’annuncio.

   Lo standard è quello di visualizzare ogni banner associato fino a quando non si dispone di una sostituzione per questo banner.

## Dati banner Companion {#companion-banner-data}

Il contenuto di un PTAdAsset descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

La notifica `PTMediaPlayerAdStartedNotification` restituisce un&#39;istanza `PTAd` che contiene una proprietà `companionAssets` (array di `PtAdAsset`).
Ogni elemento `PtAdAsset` fornisce informazioni sulla visualizzazione della risorsa.

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
   <td colname="col2"> Larghezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altezza </td> 
   <td colname="col2"> Altezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Tipo di risorsa per il banner correlato: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html I dati sono nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: I dati sono un URL iframe (src). </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">statico: I dati sono un URL statico che è un URL diretto a un'immagine. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dati </td> 
   <td colname="col2"> I dati del tipo specificato da <span class="codeph"> resourceType</span> per questo banner correlato. </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.

TVSDK fornisce un elenco di annunci banner complementari associati a un annuncio lineare tramite l&#39;evento di notifica `PTMediaPlayerAdPlayStartedNotification` .

I manifesti possono specificare annunci di banner complementari per:

* Frammento HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, TVSDK indica quali tipi sono disponibili per l’applicazione.

1. Crea un&#39;istanza `PTAdBannerView` per ogni annuncio correlato sulla pagina.

       Assicurati che siano state fornite le seguenti informazioni:
   
   * Per impedire il recupero di annunci companion di diverse dimensioni, un&#39;istanza di banner che specifica la larghezza e l&#39;altezza.
   * Dimensioni dei banner standard.

1. Aggiungi un osservatore per il `PTMediaPlayerAdStartedNotification` che esegue le seguenti operazioni:
   1. Cancella gli annunci esistenti nell&#39;istanza del banner.
   1. Ottiene l&#39;elenco degli annunci companion da `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Se l’elenco degli annunci associati non è vuoto, ripeti l’errore sopra l’elenco per le istanze del banner.

      Ogni istanza di banner ( a `PTAdAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner correlato.
   1. Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per quell’annuncio video.

      Per mostrare un annuncio di visualizzazione indipendente, aggiungi la logica al tuo script per eseguire un tag di annunci di visualizzazione normale DFP (DoubleClick for Publishers) nell’istanza di banner appropriata.
   1. Invia le informazioni sul banner a una funzione nella pagina in cui vengono visualizzati i banner in una posizione appropriata.

      In genere si tratta di una `div` e la funzione utilizza `div ID` per visualizzare il banner. Ad esempio:

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
