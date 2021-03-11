---
description: Quando il lettore multimediale passa il profilo corrente a un nuovo profilo, è possibile recuperare informazioni sullo switch, tra cui quando è stato commutato, informazioni su larghezza e altezza, o perché è stato utilizzato un bit rate diverso.
title: Ottieni informazioni sul commutatore del profilo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Ottieni informazioni sull&#39;interruttore del profilo{#get-information-about-profile-switch}

Quando il lettore multimediale passa il profilo corrente a un nuovo profilo, è possibile recuperare informazioni sullo switch, tra cui quando è stato commutato, informazioni su larghezza e altezza, o perché è stato utilizzato un bit rate diverso.

1. Ascoltare l&#39;evento `ProfileEvent.PROFILE_CHANGED`.

   Il lettore multimediale TVSDK invia questo evento quando l&#39;algoritmo di commutazione del bit rate adattivo passa a un altro profilo a causa di condizioni di rete o di macchina. (Quando cambia il bit rate o il periodo).
1. Quando si verifica l&#39;evento, controlla le seguenti proprietà per informazioni sullo switch:

   * `profile`: Identificatore per il nuovo profilo in uso.
   * `time`: Tempo di flusso in cui si è verificato l&#39;interruttore.
   * `description`: Descrizione testuale del motivo di un cambiamento del bit rate, come stringa di coppie chiave/valore separate da punto e virgola. Include un massimo di un `Reason` e un `Bitrate`. Se le informazioni non sono disponibili o il bit rate non è stato modificato, questa stringa è vuota.

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Nome chiave </th> 
      <th colname="col2" class="entry"> Valori possibili </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Motivo  </span> </td> 
      <td colname="col2"> 
       <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
       <li id="li_E374B029E1AF40689D70A9D30E057C5B">Adattamento di rete </li> 
       <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Cerca </li> 
       <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Profilo non supportato </li> 
       <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Failover </li> 
       </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Bitrate  </span> </td> 
      <td colname="col2"> 
       <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
       <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> up  </span>: Il bit rate è aumentato </li> 
       <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> giù  </span>: Il bit rate è diminuito </li> 
       </ul> </td> 
      </tr> 
    </tbody>
</table>

    Di seguito sono riportati alcuni esempi di stringhe &quot;description&quot; restituite: 
    
    &quot;
    &quot;Bitrate::=up;Motivo:=Adattamento rete;&quot;
    
    &quot;Bitrate:=down;Motivo::=Failover;&quot;
    &quot;
    
    * `width`: Intero che indica la larghezza in pixel.
    * `height`: Numero intero che indica l’altezza in pixel.
    
    >[!NOTE]
    >
    >I dati di larghezza e altezza sono disponibili solo quando sono inclusi nel tag `RESOK` nel manifesto M3U8. Se le informazioni non sono incluse nell&#39;M3U8, le proprietà larghezza e altezza sono impostate su 0, in quanto non fanno parte delle informazioni sul profilo.

<!--<a id="example_A713D420AE2E4E3CB7B78C6BC732BE90"></a>-->

Ad esempio:

```
_player.addEventListener(ProfileEvent.PROFILE_CHANGED, onProfileChange); 
private function onProfileChange(event:ProfileEvent):void { 
    _logger.info("#onProfileChange Current profile/bitrate has changed.  
      {0} for reason {1} of resolution [ {2} , {3} ]",  
      event.profile, event.description, event.width, event.height); 
}
```
