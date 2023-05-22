---
description: Browser TVSDK supporta una serie di funzioni DASH che è possibile implementare per aggiungere funzionalità alle applicazioni video.
title: Feature DASH supportate
exl-id: 29a5d1a3-e31e-459c-90b5-80227df46e4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Feature DASH supportate{#supported-dash-features}

Browser TVSDK supporta una serie di funzioni DASH che è possibile implementare per aggiungere funzionalità alle applicazioni video.

* [Funzioni di riproduzione core DASH](#dash-core-playback)
* [DASH Funzioni di riproduzione avanzate](#dash-advanced-playback)
* [DASH Funzioni di protezione del contenuto](#dash-content-protection)
* [Funzionalità di inserimento e core DASH](#dash-core-ad-insertion)
* [DASH Funzioni avanzate di inserimento annunci](#dash-advanced-insertion-features)
* [Integrazioni DASH](#dash-integrations)

>[!TIP]
>
>Nelle tabelle delle matrici di funzioni riportate di seguito,  ![](assets/supported15.png)
>indica che la funzione è supportata nella versione corrente.

Sono supportate le seguenti funzionalità:

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## Integrazioni DASH {#dash-integrations}

| Categoria | Tipo di contenuto | Funzionalità | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Integrazioni | VOD + Live | Integrazione Adobe Analytics VHL | ![](assets/supported15.png) |
| Integrazioni | VOD + Live | Fatturazione | ![](assets/supported15.png) |
| Integrazioni | VOD + Live | Sfoglia | ![](assets/supported15.png) |

## Funzionalità avanzate di inserimento annunci DASH (CSAI) {#dash-advanced-insertion-features}

| Categoria | Tipo di contenuto | Funzionalità | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | Solo annuncio | Non supportato |
| Ad Insertion | VOD | Parametri di targeting | Solo VOD |
| Ad Insertion | VOD | Parametri personalizzati | Solo VOD |
| Ad Insertion | VOD + Live | Criterio annuncio personalizzato | Non supportato |
| Ad Insertion | VOD + Live | Caricamento annuncio lazy | Non supportato |
| Ad Insertion | VOD | Annunci di accompagnamento, banner pubblicitari e annunci selezionabili | Non supportato |
| Ad Insertion | VOD | VPAID 2.0 | Non supportato |

## Funzioni di inserimento e core DASH (CSAI) {#dash-core-ad-insertion}

| Categoria | Tipo di contenuto | Funzionalità | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Live | Pre-roll | Solo VOD |
| Ad Insertion | VOD + Live | Mid-roll | Solo VOD |
| Ad Insertion | VOD + Live | Post-roll | Solo VOD |
| Ad Insertion | VOD FER | Risoluzione e comportamenti degli annunci | Non supportato |
| Ad Insertion | VOD + Live | Criterio annuncio predefinito | Solo VOD |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | Solo VOD |
| Ad Insertion | VOD + Live | VMAP 1.0 | Solo VOD |
| Ad Insertion | VOD + Live | CRS v3.1 | Solo VOD |

## Funzioni di protezione del contenuto DASH {#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Categoria </th> 
   <th colname="col2" class="entry"> Tipo di contenuto </th> 
   <th colname="col3" class="entry"> Funzionalità </th> 
   <th colname="col6" class="entry"> HTML5 FF, IE, Chrome, Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Protezione dei contenuti </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> Non supportato </td>
  </tr> 
  <tr> 
   <td colname="col1"> Protezione dei contenuti </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> Sample-AES </td> 
   <td colname="col6"> Non supportato </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Protezione dei contenuti </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevine attivato 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">Chrome </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">PlayReady in Internet Explorer su Windows 8.1 ed Edge </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Accesso Adobe per Windows Firefox (solo video) </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Funzionalità di riproduzione avanzate DASH {#dash-advanced-playback}

| Categoria | Tipo di contenuto | Funzionalità | HTML5, FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Riproduzione | VOD | Riproduzione a offset | ![](assets/supported15.png) |
| Riproduzione | VOD | Riproduzione solo audio | ![](assets/supported15.png) |
| Riproduzione | VOD | Trick play | ![](assets/supported15.png) |
| Riproduzione | VOD | Smooth Trick Play | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Analisi ID3 | Non supportato |
| Riproduzione | VOD | Supporto di più periodi | Solo VOD |
| Riproduzione | VOD + Live | Flussi token | Non supportato |
| Riproduzione | VOD + Live | Fatturazione | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Sfoglia | ![](assets/supported15.png) |

## Funzioni di riproduzione core DASH {#dash-core-playback}

| Categoria | Tipo di contenuto | Funzionalità | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Riproduzione | VOD + Live | Riproduzione generale (riproduzione, pausa, ricerca) | ![](assets/supported15.png) |
| Riproduzione | VOD FER | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato |
| Riproduzione | VOD + Live | Bitrate adattivo | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Sottotitoli 608/708 | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | WebVTT | Solo VOD |
| Riproduzione | VOD + Live | Failover | Solo VOD |
| Riproduzione | VOD + Live | Notifiche QoS e lettore | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Supporto per le intestazioni dei cookie | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Impostazione dei parametri di controllo del buffer | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Impostare i controlli del bitrate adattivo | ![](assets/supported15.png) |
| Riproduzione | VOD + Live | Tag personalizzati (EventStream) | Solo VOD (in linea) |
| Riproduzione | VOD + Live | Audio di associazione tardiva | Solo VOD |
| Riproduzione | VOD + Live | Reindirizzamento 302 | Solo VOD |
