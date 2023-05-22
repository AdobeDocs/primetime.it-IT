---
description: Quando il lettore multimediale passa a un nuovo profilo, è possibile recuperare informazioni sullo switch, tra cui quando è stato cambiato, informazioni su larghezza e altezza o perché è stato utilizzato un bitrate diverso.
title: Ottenere informazioni sul passaggio a un altro profilo
exl-id: 3ef4b319-dd78-4abd-9c2d-ab1d608f6cea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Ottenere informazioni sul passaggio a un altro profilo{#get-information-about-profile-switch}

Quando il lettore multimediale passa a un nuovo profilo, è possibile recuperare informazioni sullo switch, tra cui quando è stato cambiato, informazioni su larghezza e altezza o perché è stato utilizzato un bitrate diverso.

1. Ascolta la `AdobePSDK.PSDKEventType.PROFILE_CHANGED` evento.

   Il lettore multimediale TVSDK del browser invia questo evento quando l’algoritmo di commutazione della velocità in bit adattiva passa a un altro profilo a causa di condizioni di rete o del computer. (quando la velocità di trasmissione o il periodo cambia).
1. Quando si verifica l&#39;evento, controllare le seguenti proprietà per informazioni sull&#39;opzione:

   * `profile`: identificatore per il nuovo profilo utilizzato.
   * `time`: ora del flusso in cui si è verificato il passaggio.
   * `description`: descrizione testuale del motivo di una modifica della velocità in bit, sotto forma di stringa di coppie chiave/valore separate da punto e virgola. Include un massimo di un elemento `Reason` e uno `Bitrate`. Se le informazioni non sono disponibili o la velocità in bit non è stata modificata, la stringa è vuota.

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Nome chiave </th> 
      <th colname="col2" class="entry"> Valori possibili </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Motivo </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">Adattamento rete </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Ricerca </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Profilo non supportato </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Failover </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Bitrate </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> su </span>: velocità in bit aumentata </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> giù </span>: velocità in bit diminuita </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   Ecco alcuni esempi di restituiti `description` stringhe:

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`: numero intero che indica la larghezza in pixel.
   * `height`: numero intero che indica l’altezza in pixel.

   >[!NOTE]
   >
   >I dati di larghezza e altezza sono disponibili solo quando sono inclusi nel `RESOLUTION` nel manifesto M3U8. Se le informazioni non sono incluse in M3U8, le proprietà width e height vengono impostate su 0, in quanto non fanno parte delle informazioni del profilo.
