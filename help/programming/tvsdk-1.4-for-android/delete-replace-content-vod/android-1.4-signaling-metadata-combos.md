---
description: Puoi contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci e dalle combinazioni di metadati di annunci
exl-id: 0b265471-2d5c-432b-b1c9-c850ce99f2f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci e dalle combinazioni di metadati di annunci{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puoi contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!NOTE]
>
>In caso di conflitto tra gli intervalli di tempo e le modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

**Tabella 3: Comportamenti combinati modalità di segnalazione/metadati**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modalità di segnalazione annuncio </th> 
   <th class="entry"> Metadati annuncio </th> 
   <th class="entry"> Resolver creati </th> 
   <th class="entry"><span class="codeph"> Informazioni sul posizionamento</span> creato </th> 
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
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li><span class="codeph"> InformazioniPosizionamento (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalli eliminati, annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Sostituisci, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE), InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
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
   <td> Contrassegna, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td> <b>Cue manifesto</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> InformazioniPosizionamento (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalli eliminati, annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Contrassegna, Auditude </td> 
   <td> Contrassegna, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina </td> 
   <td> Elimina </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
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
   <td> Sostituisci, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE), InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
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
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
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
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE), InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
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
   <td> Contrassegna, Auditude </td> 
   <td> Annuncio Personalizzato, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati, nessun annuncio inserito </td> 
  </tr> 
  <tr> 
   <td> <b>Non impostato (impostazione predefinita)</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina </td> 
   <td> Elimina </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
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
   <td><span class="codeph"> InformazioniPosizionamento (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Annunci inseriti </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Sostituisci, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE), InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
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
   <td> Contrassegna, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalli contrassegnati </td> 
  </tr> 
 </tbody> 
</table>
