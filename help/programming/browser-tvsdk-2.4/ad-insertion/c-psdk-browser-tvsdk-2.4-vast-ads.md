---
description: Quando il browser TVSDK richiede un annuncio che non si trova sul server dell’annuncio principale, il lettore deve richiedere l’annuncio dal server secondario. Video Ad Server Template (VAST) imposta lo standard di comunicazione tra i server di annunci e i lettori video e rappresenta la risposta inviata dal server di annunci secondario quando l’annuncio viene richiesto.
title: VAST ads
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# VAST ads {#vast-ads}

Quando il browser TVSDK richiede un annuncio che non si trova sul server dell’annuncio principale, il lettore deve richiedere l’annuncio dal server secondario. Video Ad Server Template (VAST) imposta lo standard di comunicazione tra i server di annunci e i lettori video e rappresenta la risposta inviata dal server di annunci secondario quando l’annuncio viene richiesto.

Per ulteriori informazioni su VAST, consulta [Modello di server di annunci video digitali (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

Il browser TVSDK supporta i seguenti elementi di annunci VAST:

## Wrapper e annunci in linea {#section_11B8A1A8F52F4F77981C6AAC02185087}

Sono supportati i seguenti elementi:

* **`wrapper`** Quando il lettore deve contattare un server di annunci secondario per richiedere un annuncio, l&#39;elemento wrapper fornisce le informazioni di reindirizzamento. Un elemento wrapper può puntare a diversi wrapper che alla fine puntano a un annuncio VAST.

* **`inline`** Sono supportati i seguenti elementi obbligatori:

* `AdSystem`
* `AdTitle`
* `Impression`

  Sono supportati i seguenti elementi facoltativi:

* `Description`
* `Survey`
* `Error`

## Creatività {#section_0121F948CB074E49A8132D202786CAA4}

Questo elemento fa parte di un annuncio VAST e contiene un `creative` che può supportare un annuncio lineare, un annuncio non lineare o un annuncio correlato. In `creative` elemento, l&#39; `id`, `sequence`, e `adId` sono supportati.

Seguono ulteriori informazioni sui tipi di annunci:

* **Annunci lineari** Sono supportati i seguenti elementi:

   * `TrackingEvent`, che contiene `Tracking` elemento.
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, tra cui:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

        >[!TIP]
        >
        >In questo elemento, il `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`, e `type` Gli attributi sono supportati.

* **Annunci non lineari** Sono supportati i seguenti elementi:

   * `Non-linear`

     >[!TIP]
     >
     >In questo elemento, il `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`, e `minSuggestedDuration` Gli attributi sono supportati.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Companion ads** Sono supportati i seguenti elementi:

   * `Companion`

     >[!TIP]
     >
     >In questo elemento, il `id`, `width`, `height`, `apiFramework`, `expandedWidth`, e `expandedHeight` Gli attributi sono supportati.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Estensioni {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Sono supportate solo le estensioni specifiche per le Auditudi.

* `Extension`
