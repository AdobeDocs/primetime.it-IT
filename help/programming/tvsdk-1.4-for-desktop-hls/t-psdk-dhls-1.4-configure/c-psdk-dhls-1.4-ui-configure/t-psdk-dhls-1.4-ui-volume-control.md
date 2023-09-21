---
description: È possibile impostare un controllo dell'interfaccia utente per il volume audio.
title: Fornire il controllo volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Fornire il controllo volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume audio.

1. Attendere che l&#39;istanza MediaPlayer sia in uno stato valido per questo comando.

   Qualsiasi stato tranne RILASCIATO è valido.
1. Chiamare il metodo del set di volumi su `MediaPlayer` per impostare il volume audio.

   ```
   public function set volume(value:Number):void
   ```

   Il valore per il volume rappresenta il volume richiesto espresso come proporzione del volume massimo, dove 0 è invisibile all&#39;utente e 1 è il volume massimo.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Se il volume specificato è </th> 
      <th colname="col2" class="entry"> Il volume risultante è </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Minore di 0 </td> 
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
      <li id="li_B00BC6F4812D4000891358F762C8E492">Risultato se è compreso tra 0 e 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 se il risultato è maggiore di 1 </li> 
      </ul> <p>Suggerimento: questa logica gestisce i valori forniti dai client in base alle versioni precedenti di 
      <span class="codeph">frasi/primetime-sdk-name</span>, in cui i valori di volume variavano da 0 a 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
