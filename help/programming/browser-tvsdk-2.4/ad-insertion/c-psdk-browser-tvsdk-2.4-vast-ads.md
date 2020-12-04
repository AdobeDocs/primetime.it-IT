---
description: Quando Browser TVSDK richiede un annuncio che non si trova sul server di annunci principale, il lettore deve richiedere l'annuncio dal server secondario. Video Ad Serving Template (VAST) imposta lo standard di comunicazione tra server di annunci e lettori video ed è la risposta che viene inviata dal server di annunci secondario quando l'annuncio viene richiesto.
seo-description: Quando Browser TVSDK richiede un annuncio che non si trova sul server di annunci principale, il lettore deve richiedere l'annuncio dal server secondario. Video Ad Serving Template (VAST) imposta lo standard di comunicazione tra server di annunci e lettori video ed è la risposta che viene inviata dal server di annunci secondario quando l'annuncio viene richiesto.
seo-title: Annunci VAST
title: Annunci VAST
uuid: 052dae0c-2425-456c-aebe-531f68bb5aa8
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Annunci VAST {#vast-ads}

Quando Browser TVSDK richiede un annuncio che non si trova sul server di annunci principale, il lettore deve richiedere l&#39;annuncio dal server secondario. Video Ad Serving Template (VAST) imposta lo standard di comunicazione tra server di annunci e lettori video ed è la risposta che viene inviata dal server di annunci secondario quando l&#39;annuncio viene richiesto.

Per ulteriori informazioni su VAST, vedere [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

Il browser TVSDK supporta i seguenti elementi di annunci VAST:

## Annunci Wrapper e in linea {#section_11B8A1A8F52F4F77981C6AAC02185087}

Sono supportati i seguenti elementi:

* **`wrapper`** Quando il lettore deve contattare un server di annunci secondario per richiedere un annuncio, l&#39;elemento wrapper fornisce le informazioni di reindirizzamento. Un elemento wrapper può puntare a diversi wrapper che in ultima analisi puntano a un annuncio VAST.

* **`inline`** Sono supportati i seguenti elementi richiesti:

* `AdSystem`
* `AdTitle`
* `Impression`

   Sono supportati i seguenti elementi facoltativi:

* `Description`
* `Survey`
* `Error`

## Creativi {#section_0121F948CB074E49A8132D202786CAA4}

Questo elemento è un file che fa parte di un annuncio VAST e contiene un elemento `creative` che può supportare un annuncio lineare, un annuncio non lineare o un annuncio complementare. Nell&#39;elemento `creative` sono supportati gli elementi `id`, `sequence` e `adId`.

Ulteriori informazioni sui tipi di annunci:

* **Linear** adsSono supportati i seguenti elementi:

   * `TrackingEvent`, che contiene l&#39; `Tracking` elemento .
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, compresi i seguenti elementi:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >In questo elemento sono supportati gli attributi `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework` e `type`.

* **Annunci non lineariSono supportati** i seguenti elementi:

   * `Non-linear`

      >[!TIP]
      >
      >In questo elemento sono supportati gli attributi `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio` e `minSuggestedDuration`.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Companion** adsSono supportati i seguenti elementi:

   * `Companion`

      >[!TIP]
      >
      >In questo elemento sono supportati gli attributi `id`, `width`, `height`, `apiFramework`, `expandedWidth` e `expandedHeight`.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Estensioni {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Sono supportate solo le estensioni specifiche per l&#39;audio.

* `Extension`
