---
description: È possibile contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse modalità di segnalazione degli annunci e combinazioni di metadati degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
title: Effetto sull’inserimento e l’eliminazione degli annunci dalle combinazioni della modalità di segnalazione degli annunci e dei metadati degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Effetto sull&#39;inserimento e l&#39;eliminazione degli annunci dalle combinazioni di modalità ad Signing e metadati degli annunci{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

È possibile contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse modalità di segnalazione degli annunci e combinazioni di metadati degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!NOTE]
>
>Quando si verifica un conflitto tra intervalli di tempo e modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

**Tabella 3: Comportamenti della modalità di segnalazione/combinazione di metadati**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modalità di segnalazione degli annunci </th> 
   <th class="entry"> Metadati annuncio </th> 
   <th class="entry"> Risolutori creati </th> 
   <th class="entry"><span class="codeph"> </span> PlacementInformationScreated </th> 
   <th class="entry"> Comportamento risultante </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>Mappa del server</b> </td> 
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
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
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
   <td> Sostituisci, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Segna </td> 
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
   <td> Segna </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Sostituisci, Auditude </td> 
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
   <td> Nessuno </td> 
   <td> Nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Sostituisci, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti dagli annunci </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Segna </td> 
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
   <td> <b>Non impostato (predefinito)</b> </td> 
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
   <td> Sostituisci, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalli sostituiti dagli annunci </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Segna </td> 
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

