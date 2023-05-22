---
description: È possibile utilizzare le seguenti informazioni per personalizzare il lettore. Per ogni costrutto visivo, i comportamenti corrispondenti sono menzionati nel comportamento predefinito.
title: Scuoiamento del lettore
exl-id: 4ad50f96-d174-401f-a731-21e5fbfdbe31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Scuoiamento del lettore {#skinning-the-player}

È possibile utilizzare le seguenti informazioni per personalizzare il lettore. Per ogni costrutto visivo, i comportamenti corrispondenti sono menzionati nel comportamento predefinito.

>[!IMPORTANT]
>
>I dettagli di skin in questo documento si riferiscono agli elementi UI predefiniti creati dal framework dell&#39;interfaccia utente. Se il lettore ha modificato questi elementi, è necessario modificare anche gli elementi di skin.

## Immersioni contenitore {#section_99B0D598219D4150B57E97D5381B118F}

Di seguito sono riportati gli stili per i contenitori div:

>[!TIP]
>
>Queste immersioni sono elencate nella `common-styles.css` file.

Di seguito sono riportati gli stili per il div principale:

<table id="table_AC5745DF725543ADBBCD68BA6130DF12"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><b>Div principale</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-main-video-div-style</span> </td> 
   <td colname="col2"> <p>Stile del div principale in cui viene riprodotto il video. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .pip-mode-active</span> </td> 
   <td colname="col2"> <p>Utilizzato quando la modalità PIP è attiva. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> videoBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Picture in Picture (PIP)</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-pip-video-div</span> </td> 
   <td colname="col2"> <p>Stile del div in cui viene riprodotto il video PIP. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .view-as-main-video</span> </td> 
   <td colname="col2"> <p>Applicato al PIP iniziale dopo lo scambio e visualizzato come video principale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Visualizzazione multi-video</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-multi-view-container</span> </td> 
   <td colname="col2"> <p>Viene utilizzato nella visualizzazione multividio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-multi-view</span> </td> 
   <td colname="col2"> <p>Stile CSS comune inserito in ogni video della visualizzazione multipla. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multiview</span> </td> 
   <td colname="col2"> <p>Quando il contenitore che ospita ciascuno dei video in multiview è in multiview. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Vari controlli {#section_E9E4A8E3AEBF4BDC89840B84B3B0E737}

Di seguito sono riportati gli stili per i controlli del lettore generici:

>[!TIP]
>
>Questi stili sono elencati nella `default-controls.css` file.

<table id="table_0ACB6BAB5DAD42DBBD18CA7C0385A261"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control</span> </td> 
   <td colname="col2"> <p>Applicabile a tutti i comandi sulla barra di controllo, eccetto lo scorrimento e lo spazio </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-input-slider</span> </td> 
   <td colname="col2"> <p>Cursori di input </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-header</span> </td> 
   <td colname="col2"> <p>Intestazione dei pannelli </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-vertical-list-menu-item</span> </td> 
   <td colname="col2"> <p>Elenco menu in stile verticale </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-fill-spacer</span> </td> 
   <td colname="col2"> <p>Spazio sulla barra di controllo </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> separatore ptp-hr</span> </td> 
   <td colname="col2"> <p>Separatore di regole orizzontale </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-title</span> </td> 
   <td colname="col2"> <p>Titolo dei pannelli </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-close-btn</span> </td> 
   <td colname="col2"> <p>Pulsante per la chiusura del pannello </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-button-background</span> </td> 
   <td colname="col2"> <p>Sfondo di tutti i pulsanti </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-txt-control</span> </td> 
   <td colname="col2"> <p>Stili predefiniti per i controlli di testo. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Barra di controllo {#section_B683B51EC746484B9AA90CB481D637BD}

Di seguito sono riportati gli stili della barra di controllo:

<table id="table_681E13F264674F849FAA2523EB65F094"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control-bar</span> (comportamento predefinito)</td>
   <td colname="col2"> <p>Applicabile alla barra di controllo </p> </td> 
  </tr> 
 </tbody> 
</table>

## Pulsanti funzione {#section_57FFD242FF674EA2867BCF6CA7F6B855}

>[!NOTE]
>
>Le lettere nelle tabelle seguenti corrispondono alle lettere della figura.

Di seguito sono riportati gli stili per la barra di scorrimento:

<table id="table_2207AD72E72A47FFA03AC748F06A54FD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile (A) </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar</span> </td> 
   <td colname="col2"> <p>Barra di scorrimento sulla barra di controllo </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-buffer-progress-bar</span> </td> 
   <td colname="col2"> <p>Barra di avanzamento del buffer sulla barra di scorrimento </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-seek-to-bar</span> </td> 
   <td colname="col2"> <p>Stato della barra di scorrimento quando l’utente vi cerca </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-playback-progress-bar</span> </td> 
   <td colname="col2"> <p>Stato della barra di scorrimento nella riproduzione normale </p> </td> 
  </tr>
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-progress-bar-play-head</span> </td>
   <td colname="col2"> <p>Riproduci la testina sulla barra di scorrimento durante la riproduzione </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker-bar</span> </td>
   <td colname="col2"> <p>Barra del marcatore dell’annuncio </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker</span> </td>
   <td colname="col2"> <p>Marcatore annuncio </p> </td>
  </tr>
 </tbody>
</table>

I comportamenti predefiniti sono:

* `scrubBarBehavior`
* `bufferProgressBarBehavior`
* `playHeadBehavior`
* `playProgressBarBehavior`
* `seekToBarBehavior`

## Pulsante Riproduci/Pausa {#section_F1F40A948D0049C5A4D8EA5F2A475CAA}

Di seguito sono riportati gli stili del pulsante Riproduci/Pausa:

<table id="table_975C2293222A4782A8C75A6149C1AD27">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (B) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause</span> </td>
   <td colname="col2"> <p>Riproduci il pulsante Pausa sulla barra di controllo. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td>
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> in stato di pausa </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td> 
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> nello stato di riproduzione </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `playPauseButtonBehavior`.

## Volume {#section_23E17BD2343948F8A2CEE1C8BEE2F874}

Di seguito sono riportati gli stili per configurare il pulsante volume:

<table id="table_8F9831F36A4D427CA31C9FFA4173170D">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (C) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><span class="codeph"> .ptp-volume-control</span>
     <ul id="ul_B12ADDFB83EA40FD8B4E92AF418AA4B4">
      <li id="li_7DA8143A69ED4E7D8A560B9FF75D6BA7"><span class="codeph"> .espanso</span> </li>
      <li id="li_D8CCAD45D81C4850B6903FE261833AE6"><span class="codeph"> .verticale</span> </li>
     </ul> </p> </td>
   <td colname="col2"> <p>Controllo volume sulla barra di controllo
     <ul id="ul_2C60F018FDCB458885738AC378C02F61">
      <li id="li_6B19572B504A4BBF9C97DC29C0E92A1D">Quando il controllo è espanso </li>
      <li id="li_6489E422E1944D5194CBDFC8383D2F30">Quando il controllo è in forma verticale </li>
     </ul> </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume</span> </td>
   <td colname="col2"> <p>Pulsante Volume sulla barra di controllo </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.min-volume-state</span> </td>
   <td colname="col2"> <p>Quando il volume è nello stato minimo </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.mute-state</span> </td>
   <td colname="col2"> <p>Quando il volume è disattivato </p> </td>
  </tr>
 </tbody>
</table>

I comportamenti predefiniti sono `volumeBehavior` e `muteButtonBehavior`.

Di seguito sono riportati gli stili per il cursore volume:

<table id="table_E3DC93F8FC614C30AADAE259D18F10EF">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (D) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-slider</span> </td>
   <td colname="col2"> <p>Il dispositivo di scorrimento del volume. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-hidden</span> </td>
   <td colname="col2"> <p>Il dispositivo di scorrimento del volume in stato nascosto. </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `volumeSliderBehavior`.

## Riavvolgi {#section_06EE608FC54A4CF5B5DF9DC743CFC740}

Stile del pulsante di riavvolgimento:

<table id="table_0ACB116582D54B188E9F5B5C03D3A615">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (E) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>Pulsante di riavvolgimento sulla barra di controllo. </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `rewindButtonBehavior`.

## Ora {#section_0E6549B3DF6D4C10947D445A5F8EEA7F}

Stile per visualizzare il tempo rimanente sulla barra di controllo:

<table id="table_CEE62BFF5FB04FDCBBE1331E0D727EBA">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (F) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-txt-display-time</span> </td>
   <td colname="col2"> <p>Visualizza il tempo rimanente sulla barra di controllo </p> </td>
  </tr>
</tbody>
</table>

Il comportamento predefinito è `timeRemainingBehavior`.

## Riavvolgimento rapido {#section_F6E6C65BD3BD493A89915DF9B92933BA}

Di seguito è riportato lo stile del pulsante di riavvolgimento rapido:

<table id="table_25BB4966B709402383AB6A6822FC1999">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (G) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>Pulsante di riavvolgimento rapido sulla barra di controllo. </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `fastRewindButtonBehavior`.

## Riavvolgimento lento {#section_38A22BB8681B430F8C6808C3BD21FB4E}

Di seguito è riportato lo stile del pulsante di riavvolgimento lento:

<table id="table_E623C374622A497C91E22333D77AF8F6">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (H) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slow-wind</span> </td>
   <td colname="col2"> <p>Pulsante di riavvolgimento lento sulla barra di controllo. </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `slowRewindButtonBehavior`.

## Avanti lento {#section_92ACF092EECC4A5EAF6AA090C05E552E}

Di seguito è riportato lo stile del pulsante Avanzamento lento:

<table id="table_88C1CF5DB2D84EDBA01AC62B70509B08">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (I) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slow-forward</span> </td>
   <td colname="col2"> <p>Pulsante Avanzamento lento sulla barra di controllo. </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `slowForwardButtonBehavior`.

## Avanzamento rapido {#section_F90ED8B3739B49ACAB1F12DF18F0E4D6}

Stile per il pulsante di avanzamento rapido:

<table id="table_F166BD1E8B934B34AF3690BBBAD894B7">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile (J) </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastforward</span> </td>
   <td colname="col2"> <p>Pulsante di avanzamento rapido sulla barra di controllo. </p> </td>
  </tr>
 </tbody>
</table>

Il comportamento predefinito è `fastForwardButtonBehavior`.

## Traccia audio {#section_1CDF4FA5A1C14DB6B9C96579FFA1057C}

Di seguito sono riportati gli stili per configurare la traccia audio:

<table id="table_22FC521D786B45EB84F230894FFECE79">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Pulsante traccia audio (K)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-audio-track</span> </td>
   <td colname="col2"> <p>Pulsante traccia audio sulla barra di controllo. </p> </td>
  </tr>
  <tr>
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> audioTrackButtonBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Pannello selezione traccia audio (L)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-panel</span> </td> 
   <td colname="col2"> <p>Pannello per la selezione della traccia audio. </p> </td>
  </tr>
  <tr>
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> audioTrackSelectionPanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Intestazione selezione traccia audio (M)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>Intestazione per <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Menu di selezione traccia audio (N)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-menu</span> </td>
   <td colname="col2"> <p>Le voci di menu in <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
 </tbody>
</table>

## Condivisione {#section_B2ADC76E76304A68AD648A00A12B676E}

Di seguito sono riportati gli stili per configurare la condivisione:

<table id="table_3264C472809D462B8FC16680B96B1AC9">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Pulsante Condivisione social media (O)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video</span> </td> 
   <td colname="col2"> <p>Pulsante di condivisione social media sulla barra di controllo che si aprirà <span class="codeph"> ptp-share-video-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> shareVideoButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Condivisione del pannello video (P)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel</span> </td>
   <td colname="col2"> <p>Pannello in cui sono visualizzate le opzioni di condivisione social. </p> </td>
  </tr>
  <tr>
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> shareVideoPanelBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Menu Condivisione video (Q)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>Intestazione per <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .share-video-panel-menu</span> </td>
   <td colname="col2"> <p>Il menu in <span class="codeph"> ptp-share-video-panel</span> che mostra tutte le opzioni per condividere contenuti sui social media. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel-menu-item</span> </td>
   <td colname="col2"> <p>La voce di menu nella <span class="codeph"> share-video-panel-menu</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-facebook</span> </td>
   <td colname="col2"> <p>Voce di menu che consente di condividere contenuti su Facebook. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-twitter</span> </td>
   <td colname="col2"> <p>Voce di menu che consente di condividere contenuti su Twitter. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-google-plus</span> </td>
   <td colname="col2"> <p>Voce di menu che consente di condividere contenuti su Google Plus. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-linkedin</span> </td>
   <td colname="col2"> <p>Voce di menu che consente di condividere contenuti su LinkedIn. </p> </td>
  </tr>
 </tbody>
</table>

## Sottotitoli {#section_A01BA68218564DA0B7D6BF51F045D7AB}

Di seguito sono riportati gli stili per configurare i sottotitoli codificati:

<table id="table_777C7034C9424F8C841DABD480FFAC47">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Stile </th>
   <th colname="col2" class="entry"> Descrizione </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Pulsante Sottotitoli codificati (R)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-closed-caption</span> </td>
   <td colname="col2"> <p>Il <span class="uicontrol"> Sottotitoli</span> sulla barra di controllo. </p> </td>
  </tr>
  <tr>
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> closedCaptionButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .on-state</span> </td>
   <td colname="col2"> <p>I sottotitoli sono stati abilitati per un video. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Pannello Sottotitoli (S)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-panel</span> </td>
   <td colname="col2"> <p>Pannello per sottotitoli. </p> </td>
  </tr>
  <tr>
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> closedCaptionLanguagePanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Lingue sottotitoli codificati (T)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-panel:</span> </td>
   <td colname="col2"> <p>Intestazione per <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-menu: </span> </td>
   <td colname="col2"> <p>Il menu nel pannello sottotitoli. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Opzioni sottotitoli codificati (U)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-btn</span> </td>
   <td colname="col2"> <p>Il <span class="uicontrol"> Opzioni</span> nel pannello opzioni sottotitoli. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-panel</span> </td>
   <td colname="col2"> <p>Il pannello Opzioni nel pannello sottotitoli. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-menu-item</span> </td>
   <td colname="col2"> <p>Voce di menu nel pannello sottotitoli. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .selected</span> </td>
   <td colname="col2"> <p>Nello stato selezionato. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-done-btn</span> </td> 
   <td colname="col2"> <p>Il <span class="uicontrol"> Fine</span> nell’intestazione del pannello delle opzioni dei sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-menu</span> </td> 
   <td colname="col2"> <p>Il menu Opzioni in sottotitoli codificati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-main-menu</span> </td> 
   <td colname="col2"> <p>Il menu principale per le opzioni sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-sub-menu</span> </td> 
   <td colname="col2"> <p>Il sottomenu per le opzioni sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-opacity-slider</span> </td> 
   <td colname="col2"> <p>Cursore di opacità per le opzioni sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-separator</span> </td> 
   <td colname="col2"> <p>Il separatore delle opzioni dei sottotitoli codificati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-item</span> </td> 
   <td colname="col2"> <p>Didascalia chiusa <span class="uicontrol"> Opzioni</span> voce di menu. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-preview-panel</span> </td> 
   <td colname="col2"> <p>Pannello di anteprima sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-footer</span> </td> 
   <td colname="col2"> <p>Piè di pagina delle opzioni sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-reset-button</span> </td> 
   <td colname="col2"> <p>Il <span class="uicontrol"> Reimposta</span> nel piè di pagina del pannello opzioni sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-apply-button</span> </td> 
   <td colname="col2"> <p>Il <span class="uicontrol"> Applica</span> nel piè di pagina del pannello opzioni sottotitoli. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> closedCaptionOptionsPanelBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## Altre opzioni (V) {#section_18E25CF8A8964FFD9026A8A833089CE3}

Di seguito sono riportati gli stili per configurare opzioni aggiuntive:
<table id="table_EC6EF88E2EDE4B8EBB1C14F87A6161FA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options</span> </td> 
   <td colname="col2"> <p>Il <span class="uicontrol"> Altre opzioni</span> pulsante. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options.ptp-control-bar-btn</span> </td> 
   <td colname="col2"> <p>Il <span class="codeph"> ptp-btn-more-options</span> utilizzati nella barra di controllo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel</span> </td> 
   <td colname="col2"> <p>Il pannello di controllo Altre opzioni. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu</span> </td> 
   <td colname="col2"> <p>Il menu del pannello di controllo Altre opzioni. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu-item</span> </td> 
   <td colname="col2"> <p>La voce di menu del pannello di controllo Altre opzioni. </p> </td> 
  </tr> 
 </tbody> 
</table>

Il comportamento predefinito è `moreOptionsButtonBehavior`.

## Pulsante PIP (W) {#section_1EE039DEA99541D391B30BD1DF72A83E}

Stile per il [!UICONTROL PIP<] pulsante:

<table id="table_EE2E882C87E24D39B8D5347686F29E55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-pip</span> </td> 
   <td colname="col2"> <p>Pulsante PIP sulla barra di controllo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> pipButtonBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## Schermo Intero (X) {#section_158A19DFB30E4432A67E4A74A7CBA563}

Di seguito è riportato lo stile per configurare lo schermo intero:

<table id="table_5941835F31AC4E9CBA9702AB8D813B8F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-fullscreen</span> </td> 
   <td colname="col2"> <p>Il <span class="uicontrol"> Schermo intero</span> sulla barra di controllo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Il comportamento predefinito è `fullScreenButtonBehavior`.

## Trick Play (Y) {#section_AE6F83BB7EE2497FB13CD94A8316192D}

Di seguito è riportato lo stile per configurare la riproduzione con trucco:

<table id="table_F1ADAC0A4B4E48669828690BDEB4BC09"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> PTP-control-bar-trick-play-rate</span> </td> 
   <td colname="col2"> <p>Il componente per la visualizzazione della velocità di selezione nella barra di controllo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Il comportamento predefinito è `trickPlayRateDisplayBehavior`.

## Vista multipla (Z) {#section_58EFAE7263BA45D3A4E2AB7309A9CAA7}

Di seguito è riportato lo stile per configurare la visualizzazione multipla:

<table id="table_84B37D7410EE40DFA7A8BB8431C6DCF0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-multiview</span> </td> 
   <td colname="col2"> <p>Il <span class="uicontrol"> MultiView</span> sulla barra di controllo e lo stato iniziale di <span class="uicontrol"> Vista multipla</span> pulsante. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Il comportamento predefinito è <span class="codeph"> multiViewButtonBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
 </tbody> 
</table>

## Miniatura {#section_0AFD932975634BB08387EEE7D3BFC438}

Di seguito è riportato lo stile per configurare le miniature:

<table id="table_968136A8BBA042A7A8E79739B8F92F55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-progress-bar-thumb-nail</span> </td> 
   <td colname="col2"> <p>Barra di avanzamento delle miniature. </p> </td> 
  </tr> 
 </tbody> 
</table>

Il comportamento predefinito è `thumbnailPreviewBehavior`.

## Messaggi di errore {#section_AC9858EE1B5A4FF4947E383C663B6AB5}

Di seguito è riportato lo stile per configurare i messaggi di errore:

<table id="table_7F4C156170DB4AFFA7DEE06F00449506"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel</span> </td> 
   <td colname="col2"> <p>Pannello in cui vengono visualizzati i messaggi di errore del lettore. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-icon</span> </td> 
   <td colname="col2"> <p>L’icona visualizzata sul pannello quando viene visualizzato un messaggio di errore. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-message</span> </td> 
   <td colname="col2"> <p>Messaggio di errore visualizzato. </p> </td> 
  </tr> 
 </tbody> 
</table>

Il comportamento predefinito è `errorMessagePanelBehavior`.

## Sovrapposizione buffering {#section_2FE8FDE2599E42BAA7411D0D38FA0A88}

Di seguito è riportato lo stile per configurare le miniature:

<table id="table_1FECE1DC29B8434B886751A29455F004"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-buffering-overlay</span> </td> 
   <td colname="col2"> <p>Il controllo di sovrapposizione del buffering. </p> </td> 
  </tr> 
 </tbody> 
</table>

La sovrapposizione predefinita è `bufferingOverlayBehavior`.

## Selettori specifici {#section_51F735AEF82E41E890FF59E031A0DB89}

Stile per il pulsante di avanzamento rapido:

<table id="table_E77EDC7D227348E79C7E73FB5D46F992"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stile </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ad-break</span> </td> 
   <td colname="col2"> <p>Lo stato del pannello di controllo durante la riproduzione dell’annuncio. </p> <p>Si applica a: 
     <ul id="ul_D5076303DCD94D968682289823D1A9F2"> 
      <li id="li_4290C4B2D48546E3AD023BED6CAAE395"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_72A3D3E916E44A55BA170407EAB0527D"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_A0BAEBB0E01B402EB83E3CE9B92B15CC"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_FDF2CEDB0A854098907FF9CBCF1A61C1"><span class="codeph"> .ptp-btn-slow-forward</span> </li> 
      <li id="li_CD2E14DB3DD64C10A253DA23FBE04A04"><span class="codeph"> .ptp-btn-slow-forward</span> </li> 
      <li id="li_A230359E8F7F4571A9EBFF0E4C2462D7"><span class="codeph"> .ptp-btn-slow-wind</span> </li> 
      <li id="li_5711A315872F4FA59FDDF0EF0AFD03C6"><span class="codeph"> .ptp-btn-more-options </span> </li> 
      <li id="li_71C8E76077A84ED590160AB5ABFCC0D7"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_4A3113C0360F4F708AAA96AB316FA057"><span class="codeph"> .ptp-btn-closed-caption </span> </li> 
      <li id="li_901A0186D65A48A1B774DC555CEC5367"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
      <li id="li_2331583C01C2482B8EE72979FBF111DB"><span class="codeph"> .ptp-btn-pip </span> </li> 
      <li id="li_7BB39BDF5E294AEB8FA3DCD9F9A29468"><span class="codeph"> .ptp-btn-rewind</span> </li> 
      <li id="li_E4FEF5A7486A40F6A5FE1119BD63AFEF"><span class="codeph"> .ptp-scrub-bar</span> </li> 
      <li id="li_12153547558A4871842EE0416BCCA8B2"><span class="codeph"> .ptp-seek-to-bar</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multi-view</span> </td> 
   <td colname="col2"> <p>Stato del controllo in visualizzazione multiview. </p> <p>Si applica a: 
     <ul id="ul_A8AC653C30814AC49041F3B58A2106F4"> 
      <li id="li_0407167DA21647A8A6960DFE55A33F42"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_EA71CAF41CDC41DE859A85CE482BE97C"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_F3A998C51A034C22A914EAEFF19FFEA7"><span class="codeph"> .ptp-btn-closed-caption</span> </li> 
      <li id="li_022F871ABC894C9BA879B3AF3D341202"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .fullscreen-state</span> </td> 
   <td colname="col2"> <p>Il lettore è in modalità a schermo intero. </p> <p>Si applica a: 
     <ul id="ul_B235C1D339F64B2FAC6BC72F03807616"> 
      <li id="li_6E050EE74C604FDAB4C9C0447F547A9D"><span class="codeph"> .ptp-control-bar </span> </li> 
      <li id="li_67D54B1A41764B2DA544479CDA1C901C"><span class="codeph"> .ptp-btn-fullscreen</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
