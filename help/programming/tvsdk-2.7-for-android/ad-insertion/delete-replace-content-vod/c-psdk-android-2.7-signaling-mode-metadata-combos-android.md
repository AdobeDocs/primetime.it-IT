---
description: Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
seo-description: Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
seo-title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci
title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci
uuid: 7b2a5588-110d-4ce5-aa9c-706d357f211d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Effetto sull&#39;inserimento e l&#39;eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!TIP]
>
>In caso di conflitto tra intervalli di tempo e modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

Nella tabella seguente sono riportati i dettagli relativi alla modalità di segnalazione e ai comportamenti di combinazione di metadati:

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
 <thead> 
  <tr> 
   <th class="entry"> Modalità di segnalazione annunci </th> 
   <th class="entry"> Aggiungi metadati </th> 
   <th class="entry"> Risolutori creati </th> 
   <th class="entry"><span class="codeph"> PlacementInformation</span> screated </th> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalli eliminati </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Elimina, Auditude </td> 
   <td> Elimina, Auditude </td> 
   <td> 
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Cue Manifesto</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Not set (predefinito)</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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

