---
description: Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
seo-description: Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
seo-title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci
title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci
uuid: c2ae8148-889d-46ae-848a-5f45d993a0e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!NOTE]
>
>In caso di conflitto tra intervalli di tempo e modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

**Tabella 4: Modalità di segnalazione/Combinazione di metadati**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modalità di segnalazione annunci </th> 
   <th class="entry"> Aggiungi metadati </th> 
   <th class="entry"> Risolutori creati </th> 
   <th class="entry"><span class="codeph"> PlacementInformation</span> create </th> 
   <th class="entry"> Comportamento risultante </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>Mappa server</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> Elimina </td> 
   <td> Elimina </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalli eliminati, Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Replace, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Contrassegna </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td> <b>Cue Manifesto</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalli eliminati, annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina </td> 
   <td> Elimina </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Contrassegna </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Replace, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti </td> 
  </tr> 
  <tr> 
   <td> <b>Intervallo di tempo personalizzato</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina </td> 
   <td> Elimina </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> None </td> 
   <td> Nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Replace, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti con annunci </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Contrassegna </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Annuncio personalizzato, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td> <b>Not set (predefinito)</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina </td> 
   <td> Elimina </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Intervalli eliminati, annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Replace, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti con annunci </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Contrassegna </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
 </tbody> 
</table>

