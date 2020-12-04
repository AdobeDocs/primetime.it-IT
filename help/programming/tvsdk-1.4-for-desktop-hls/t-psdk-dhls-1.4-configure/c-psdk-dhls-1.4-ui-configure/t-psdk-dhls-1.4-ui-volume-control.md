---
description: È possibile impostare un controllo dell'interfaccia utente per il volume del suono.
seo-description: È possibile impostare un controllo dell'interfaccia utente per il volume del suono.
seo-title: Controllo del volume
title: Controllo del volume
uuid: c51e99b6-efd1-414e-9ef7-77bd53e0d6c0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# Controllo volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume del suono.

1. Attendere che l&#39;istanza di MediaPlayer sia in uno stato valido per questo comando.

   Qualsiasi stato tranne RELEASED è valido.
1. Chiamate il metodo set di volumi sull&#39;istanza `MediaPlayer` per impostare il volume audio.

   ```
   public function set volume(value:Number):void
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove 0 è invisibile e 1 è il volume massimo.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Se il volume specificato è </th> 
      <th colname="col2" class="entry"> Il volume risultante è </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Inferiore a 0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Tra 0 e 1 </td> 
      <td colname="col2"> Il volume specificato </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Maggiore di 1 </td> 
      <td colname="col2"> Il valore diviso per 100 e impostato su uno dei seguenti valori: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">Il risultato è compreso tra 0 e 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 se il risultato è maggiore di 1 </li> 
      </ul> <p>Suggerimento:  Questa logica gestisce i valori forniti dai client in base alle versioni precedenti del 
      <span class="codeph">frasi/primetime-sdk-name</span>, dove i valori del volume erano compresi tra 0 e 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
