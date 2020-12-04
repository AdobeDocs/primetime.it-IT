---
description: Browser TVSDK supporta una serie di funzioni HLS che potete implementare per aggiungere funzionalità alle applicazioni video.
seo-description: Browser TVSDK supporta una serie di funzioni HLS che potete implementare per aggiungere funzionalità alle applicazioni video.
seo-title: Funzioni HLS supportate
title: Funzioni HLS supportate
uuid: 033d81f8-cea4-4687-b2fb-1524d9164d39
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---


# Funzioni HLS supportate {#supported-hls-features}

Browser TVSDK supporta una serie di funzioni HLS che potete implementare per aggiungere funzionalità alle applicazioni video.

* [Riproduzione HLS Core](#hls-core-playback)
* [HLS Funzioni avanzate di riproduzione](#hls-advanced-playback)
* [Funzioni di protezione dei contenuti HLS](#hls-content-protection)
* [Funzioni di inserimento di annunci chiave HLS](#hls-core-ad-insertion)
* [HLS Funzioni avanzate di inserimento annunci](#hls-advanced-ad-insertion)
* [Integrazioni HLS](#hls-integrations)

>[!TIP]
>
>Nelle tabelle della matrice di funzioni riportate di seguito, l&#39;icona ![supportata](assets/supported15.png) indica che la funzione è supportata nella versione corrente.

>[!TIP]
>
>Nella colonna &quot;Limitazione piattaforma&quot; di Safari, il caso d’uso non è supportato perché la piattaforma non consente l’implementazione del supporto. Nel caso di un inserimento, utilizzare SSAI. Se vi sono limitazioni di riproduzione importanti, forzate il fallback sull&#39;Flash in Safari finché la piattaforma non supporterà il caso di utilizzo dell&#39;inserzione di annunci.

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

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integrazioni | VOD + Live | Integrazione  Adobe Analytics VHL | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Funzioni avanzate di inserimento annunci (CSAI) HLS {#hls-advanced-ad-insertion}

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion  | VOD | Solo annunci | Non supportato | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion  | VOD + Live | Parametri di targeting | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion  | VOD + Live | Criterio annunci personalizzato | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion  | VOD + Live | Lazy e caricamento | ![icona supportata](assets/supported15.png) | Non supportato | Limitazione piattaforma |
| Ad Insertion  | VOD | Annunci pubblicitari, annunci per banner e annunci cliccabili | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion  | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funzioni principali di inserimento annunci (CSAI) HLS {#hls-core-ad-insertion}

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion  | VOD + Live | Pre-roll | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion  | VOD + Live | Media roll | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion  | VOD + Live | Post-roll | Solo VOD | Solo VOD | Solo VOD |
| Ad Insertion  | FER VOD | Risoluzione degli annunci e comportamenti | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion  | VOD + Live | Criterio annunci predefinito | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Ad Insertion  | VOD + Live | VAST 2.0/3.0 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion  | VOD + Live | VMAP 1.0 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Ad Insertion  | VOD + Live | CRS v3.1 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Funzioni di protezione del contenuto HLS {#hls-content-protection}

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Protezione dei contenuti | VOD + Live | AES-128 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Protezione dei contenuti | VOD + Live | Sample-AES | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Protezione dei contenuti | VOD | DRM |  accesso al Adobe | Non supportato | FairPlay |

## Funzioni avanzate di riproduzione HLS {#hls-advanced-playback}

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD | Riproduzione a offset | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Riproduzione solo audio | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Gioco di mattoni | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD | Smooth trucco | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Analisi ID3 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Non supportato |
| Riproduzione | VOD + Live | Supporto dei marcatori di discontinuità | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Flussi token | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Fatturazione | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Browserify | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |

## Riproduzione di base HLS {#hls-core-playback}

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD + Live | Riproduzione generale (Riproduci, Pausa, Cerca) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | FER VOD | Riproduzione generale (Riproduci, Pausa, Cerca) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Bitrate adattivo | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | 608/708 didascalie | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | WebVTT | ![icona supportata](assets/supported15.png) | Solo VOD | Solo VOD |
| Riproduzione | VOD + Live | Failover manifesto | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) |
| Riproduzione | VOD + Live | Failover avanzato | ![icona supportata](assets/supported15.png) | Solo VOD | Limitazione piattaforma |
| Riproduzione | VOD + Live | Notifiche QoS e del lettore | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Supporto QoS limitato |
| Riproduzione | VOD + Live | Supporto per le intestazioni dei cookie | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Impostazione dei parametri di controllo del buffer | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Impostare i controlli di bitrate adattivi | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Tag personalizzati | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Connessione audio ritardata | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |
| Riproduzione | VOD + Live | Reindirizzamento 302 | ![icona supportata](assets/supported15.png) | ![icona supportata](assets/supported15.png) | Limitazione piattaforma |