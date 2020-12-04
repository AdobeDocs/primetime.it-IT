---
description: Sui dispositivi che supportano l'accelerazione GPU (hardware), potete utilizzare un oggetto flash.media.StageVideo per elaborare video direttamente sull'hardware del dispositivo.
seo-description: Sui dispositivi che supportano l'accelerazione GPU (hardware), potete utilizzare un oggetto flash.media.StageVideo per elaborare video direttamente sull'hardware del dispositivo.
seo-title: Requisiti minimi di StageVideo
title: Requisiti minimi di StageVideo
uuid: 8916dbac-33e0-4efd-8105-9ddbc85f0a3f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Requisiti minimi di StageVideo{#stagevideo-minimum-requirements}

Sui dispositivi che supportano l&#39;accelerazione GPU (hardware), potete utilizzare un oggetto flash.media.StageVideo per elaborare video direttamente sull&#39;hardware del dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Una combinazione di fattori diversi determina quando e come utilizzare `StageVideo`. Nella tabella seguente è riportato un&#39;istantanea di alcuni dei requisiti e delle restrizioni associati all&#39;utilizzo di StageVideo. Tali requisiti e restrizioni sono soggetti a modifiche.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Piattaforma </th> 
   <th colname="col2" class="entry"> Windows e Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Almeno l'Flash 10.1 o successivo </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Per la funzione di riserva del software, Flash 15 e versioni successive </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Browser e <span class="codeph"> impostazioni wmode</span> </td> 
   <td colname="col2"> <p><b>All'Flash 15</b>, impostate  <span class="codeph"> wmode=</span> opaqueso in modo da poter utilizzare le sovrapposizioni HTML. </p> <p>I seguenti browser attualmente non supportano l'accelerazione hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox su Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome prima 26 e qualsiasi versione di Chrome su Windows XP e Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (tutte le versioni) </li> 
     </ul>Altre combinazioni di browser/sistema operativo potrebbero impedire l'accesso all'accelerazione hardware. In questi scenari, <span class="codeph"> StageVideo</span> rientra nel software con un impatto negativo sulle prestazioni. </p> <p><b>A Flash 14 e versioni precedenti</b>, se il browser non supporta l’accelerazione hardware, il lettore Flash può eseguire il rendering direttamente sulla GPU, ma impostare  <span class="codeph"> wmode=</span> direct per abilitare questo rendering. <p>Suggerimento:  È possibile che i driver GPU di età superiore al 2009 debbano essere aggiornati in quanto potrebbero non essere supportati per l'accelerazione hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Oggetto NetStream </td> 
   <td colname="col2">L'evento <span class="codeph"> StageVideoEvent.RENDER_STATE</span> viene inviato solo se si associa un oggetto <span class="codeph"> NetStream</span> all'oggetto <span class="codeph"> StageVideo</span>. </td> 
  </tr> 
 </tbody> 
</table>

