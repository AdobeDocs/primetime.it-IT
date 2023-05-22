---
description: Puoi contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci e dalle combinazioni di metadati di annunci
exl-id: 949ca84f-4aa9-4668-b91b-99fdf13f625c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci e dalle combinazioni di metadati di annunci {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puoi contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!TIP]
>
>In caso di conflitto tra gli intervalli di tempo e le modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

La tabella seguente fornisce i dettagli relativi alla modalità di segnalazione e ai comportamenti di combinazione dei metadati:

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
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
   <td colname="1"> <p><b>Mappa server</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> InformazioniPosizionamento (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Cue manifesto</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> InformazioniPosizionamento (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> InformazioniPosizionamento (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Intervallo di tempo personalizzato</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td colname="1"> <p><b>Non impostato (impostazione predefinita)</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
