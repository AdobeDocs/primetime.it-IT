---
description: Browser TVSDK supporta una serie di funzioni HLS che è possibile implementare per aggiungere funzionalità alle applicazioni video.
title: Funzioni HLS supportate
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Funzioni HLS supportate {#supported-hls-features}

Browser TVSDK supporta una serie di funzioni HLS che è possibile implementare per aggiungere funzionalità alle applicazioni video.

* [Riproduzione core HLS](#hls-core-playback)
* [Funzioni di riproduzione avanzate HLS](#hls-advanced-playback)
* [Funzioni di protezione del contenuto HLS](#hls-content-protection)
* [Funzioni di inserimento e core HLS](#hls-core-ad-insertion)
* [Funzioni avanzate di inserimento annunci HLS](#hls-advanced-ad-insertion)
* [Integrazioni HLS](#hls-integrations)

>[!TIP]
>
>Nelle tabelle delle matrici di funzioni riportate di seguito, ![icona supportata](assets/supported15.png) indica che la funzione è supportata nella versione corrente.

>[!TIP]
>
>Nella colonna Safari, &quot;Platform Limitation&quot; significa che il caso d’uso non è supportato perché tale piattaforma non consente l’implementazione del supporto per essa. In caso di inserimento, utilizzare SSAI. Se esistono limitazioni di riproduzione importanti per te, forza il fallback al Flash su Safari fino a quando la piattaforma non supporta il caso d’uso di inserimento dell’annuncio.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

Sono supportate le seguenti funzionalità:

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## Integrazioni HLS {#hls-integrations}

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integrazioni | VOD + Live | Integrazione Adobe Analytics VHL | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Funzioni avanzate di inserimento annunci HLS (CSAI) {#hls-advanced-ad-insertion}

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Solo annuncio | Non supportato | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | Parametri di targeting | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | Criterio annuncio personalizzato | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion | VOD + Live | Caricamento annuncio lazy | ![icona supportata](assets/supported15.png) | Non supportato | Limitazione piattaforma |
| Ad Insertion | VOD | Annunci aziendali, banner pubblicitari e annunci cliccabili | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funzioni di inserimento annunci core HLS (CSAI) {#hls-core-ad-insertion}

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Live | Pre-roll | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | Mid-roll | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion | VOD + Live | Post-roll | Solo VOD | Solo VOD | Solo VOD |
| Ad Insertion | VOD FER | Risoluzione e comportamenti degli annunci | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion | VOD + Live | Criterio annuncio predefinito | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | VMAP 1.0 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | CRS v3.1 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Funzioni di protezione dei contenuti HLS {#hls-content-protection}

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Protezione dei contenuti | VOD + Live | AES-128 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Protezione dei contenuti | VOD + Live | Sample-AES | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Protezione dei contenuti | VOD | DRM | Accesso Adobe | Non supportato | FairPlay |

## Funzioni di riproduzione avanzate HLS {#hls-advanced-playback}

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD | Riproduzione a offset | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Riproduzione solo audio | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Trick play | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Funzione &quot;Smooth trick play&quot; | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Analisi ID3 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Non supportato |
| Riproduzione | VOD + Live | Supporto per marcatori di discontinuità | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Flussi token | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Fatturazione | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Sfoglia | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Riproduzione core HLS {#hls-core-playback}

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD + Live | Riproduzione generale (riproduzione, pausa, ricerca) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD FER | Riproduzione generale (riproduzione, pausa, ricerca) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Bitrate adattivo | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Sottotitoli 608/708 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | WebVTT | ![icona supportata](assets/supported15.png) | Solo VOD | Solo VOD |
| Riproduzione | VOD + Live | Failover del manifesto | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Failover avanzato | ![icona supportata](assets/supported15.png) | Solo VOD | Limitazione piattaforma |
| Riproduzione | VOD + Live | Notifiche QoS e lettore | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Supporto QoS limitato |
| Riproduzione | VOD + Live | Supporto per le intestazioni dei cookie | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Impostazione dei parametri di controllo del buffer | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Impostare i controlli del bitrate adattivo | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Tag personalizzati | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Audio di associazione tardiva | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Reindirizzamento 302 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
