---
description: Il browser TVSDK supporta una serie di funzioni HLS che è possibile implementare per aggiungere funzionalità alle applicazioni video.
title: Funzioni HLS supportate
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Funzioni HLS supportate {#supported-hls-features}

Il browser TVSDK supporta una serie di funzioni HLS che è possibile implementare per aggiungere funzionalità alle applicazioni video.

* [Riproduzione HLS Core](#hls-core-playback)
* [Funzioni di riproduzione avanzate HLS](#hls-advanced-playback)
* [Funzioni di protezione dei contenuti HLS](#hls-content-protection)
* [Funzioni di inserimento degli annunci principali di HLS](#hls-core-ad-insertion)
* [Funzioni avanzate di inserimento annunci HLS](#hls-advanced-ad-insertion)
* [Integrazioni HLS](#hls-integrations)

>[!TIP]
>
>Nelle tabelle della matrice delle funzioni seguenti, ![icona supportata](assets/supported15.png) indica che la funzione è supportata nella versione corrente.

>[!TIP]
>
>Nella colonna Safari &quot;Limitazione piattaforma&quot; il caso d’uso non è supportato perché la piattaforma non consente l’implementazione del supporto per tale piattaforma. Nel caso di un inserimento, utilizzare SSAI. Se sono presenti limitazioni di riproduzione importanti per te, forza il fallback su Flash su Safari fino a quando la piattaforma non supporta il caso di utilizzo dell’inserimento di annunci.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

Sono supportate le seguenti funzioni:

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

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integrazioni | VOD + Live | Integrazione Adobe Analytics VHL | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Funzioni avanzate di inserimento annunci HLS (CSAI) {#hls-advanced-ad-insertion}

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Solo annuncio | Non supportato | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | Parametri di targeting | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | Criterio annuncio personalizzato | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Ad Insertion | VOD + Live | Lazy annuncio caricamento | ![icona supportata](assets/supported15.png) | Non supportato | Limitazione della piattaforma |
| Ad Insertion | VOD | Annunci Companion, Annunci Banner e Annunci Clickable | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funzioni principali di inserimento degli annunci HLS (CSAI) {#hls-core-ad-insertion}

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Live | Pre-roll | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | Mid-roll | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Ad Insertion | VOD + Live | Post-roll | Solo VOD | Solo VOD | Solo VOD |
| Ad Insertion | FER VOD | Risoluzione degli annunci e comportamenti | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Ad Insertion | VOD + Live | Criterio annuncio predefinito | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | VMAP 1.0 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion | VOD + Live | CRS v3.1 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Funzioni di protezione dei contenuti HLS {#hls-content-protection}

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Protezione dei contenuti | VOD + Live | AES-128 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Protezione dei contenuti | VOD + Live | Sample-AES | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Protezione dei contenuti | VOD | DRM | Accesso Adobe | Non supportato | FairPlay |

## Funzioni di riproduzione avanzate HLS {#hls-advanced-playback}

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD | Riproduzione a offset | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Riproduzione solo audio | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Gioco di mattoni | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Giochi a carte liscio | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Analisi ID3 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Non supportato |
| Riproduzione | VOD + Live | Supporto per marker discontinuità | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Flussi token | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Fatturazione | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Navigare | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Riproduzione principale HLS {#hls-core-playback}

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD + Live | Riproduzione generale (riproduzione, pausa, ricerca) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | FER VOD | Riproduzione generale (riproduzione, pausa, ricerca) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Bit rate adattivo | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | sottotitoli 608/708 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | WebVTT | ![icona supportata](assets/supported15.png) | Solo VOD | Solo VOD |
| Riproduzione | VOD + Live | Failover manifesto | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Failover avanzato | ![icona supportata](assets/supported15.png) | Solo VOD | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Notifiche di QoS e del lettore | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Supporto QoS limitato |
| Riproduzione | VOD + Live | Supporto per le intestazioni dei cookie | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Impostazione dei parametri di controllo del buffer | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Imposta i controlli del bit rate adattivo | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Tag personalizzati | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Audio con associazione ritardata | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |
| Riproduzione | VOD + Live | Reindirizzamento 302 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione della piattaforma |