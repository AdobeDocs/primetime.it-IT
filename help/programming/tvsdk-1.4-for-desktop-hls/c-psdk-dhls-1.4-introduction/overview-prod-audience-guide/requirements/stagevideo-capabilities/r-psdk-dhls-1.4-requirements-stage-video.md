---
description: Sui dispositivi che supportano l'accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare i video direttamente sull'hardware del dispositivo.
title: Requisiti minimi di StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Requisiti minimi di StageVideo{#stagevideo-minimum-requirements}

Sui dispositivi che supportano l&#39;accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare i video direttamente sull&#39;hardware del dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Una combinazione di fattori diversi determina quando e come utilizzare `StageVideo`. La tabella seguente presenta un’istantanea di alcuni dei requisiti e delle restrizioni associati all’utilizzo di StageVideo. Tali requisiti e restrizioni sono soggetti a modifiche.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Piattaforma </th> 
   <th colname="col2" class="entry"> Windows e Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> giocatore di Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Almeno il Flash 10.1 o successivo </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Per la funzione di fallback to software, Flash 15 e versioni successive </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Browser e impostazioni <span class="codeph"> wmode</span> </td> 
   <td colname="col2"> <p><b>Al Flash 15</b>, imposta  <span class="codeph"> wmode=</span> opaqueso per poter utilizzare le sovrapposizioni HTML. </p> <p>I seguenti browser attualmente non supportano l'accelerazione hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox su Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome prima 26 e qualsiasi versione di Chrome su Windows XP e Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (tutte le versioni) </li> 
     </ul>Altre combinazioni browser/sistema operativo potrebbero impedire l'accesso all'accelerazione hardware. In questi scenari, <span class="codeph"> StageVideo</span> rientra nel software con un impatto negativo sulle prestazioni. </p> <p><b>Al Flash 14 e versioni precedenti</b>, se il browser non supporta l’accelerazione hardware, il lettore di Flash può eseguire il rendering direttamente nella GPU, ma impostare  <span class="codeph"> wmode=</span> directing per abilitare questo rendering. <p>Suggerimento:  È possibile che sia necessario aggiornare i driver GPU con età superiore al 2009, in quanto potrebbero mancare il supporto per l'accelerazione hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Oggetto NetStream </td> 
   <td colname="col2">L'evento <span class="codeph"> StageVideoEvent.RENDER_STATE</span> viene inviato solo se si collega un oggetto <span class="codeph"> NetStream</span> all'oggetto <span class="codeph"> StageVideo</span>. </td> 
  </tr> 
 </tbody> 
</table>

