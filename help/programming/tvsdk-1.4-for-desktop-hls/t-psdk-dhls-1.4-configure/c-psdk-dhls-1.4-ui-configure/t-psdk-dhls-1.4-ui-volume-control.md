---
description: È possibile impostare un controllo dell'interfaccia utente per il volume sonoro.
title: Controllo del volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Fornire il controllo del volume{#provide-volume-control}

È possibile impostare un controllo dell&#39;interfaccia utente per il volume sonoro.

1. Attendi che l&#39;istanza MediaPlayer sia in uno stato valido per questo comando.

   Qualsiasi stato tranne RELEASED è valido.
1. Chiama il metodo set di volumi sull&#39;istanza `MediaPlayer` per impostare il volume audio.

   ```
   public function set volume(value:Number):void
   ```

   Il valore per il volume rappresenta il volume richiesto espresso in proporzione al volume massimo, dove 0 è silenzioso e 1 è il volume massimo.

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
      <td colname="col2"> Volume specificato </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Maggiore di 1 </td> 
      <td colname="col2"> Il valore diviso per 100 e impostato su uno dei seguenti valori: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">Il risultato se è compreso tra 0 e 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 se il risultato è maggiore di 1 </li> 
      </ul> <p>Suggerimento:  Questa logica gestisce i valori forniti dai client in base alle versioni precedenti di 
      <span class="codeph">frasi/primetime-sdk-name</span>, dove i valori del volume variano da 0 a 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
