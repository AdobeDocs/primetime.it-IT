---
description: Sui dispositivi che supportano l'accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare video direttamente sull'hardware del dispositivo.
title: Requisiti minimi di StageVideo
exl-id: f401682d-c47d-4284-8832-293515a76581
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Requisiti minimi di StageVideo{#stagevideo-minimum-requirements}

Sui dispositivi che supportano l&#39;accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare video direttamente sull&#39;hardware del dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Una combinazione di fattori diversi determina quando e come utilizzare `StageVideo`. Nella tabella seguente viene fornita un&#39;istantanea di alcuni requisiti e restrizioni associati all&#39;utilizzo di StageVideo. Tali requisiti e restrizioni sono soggetti a modifiche.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Piattaforma </th> 
   <th colname="col2" class="entry"> Sistema operativo Windows e Mac </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Lettore Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Almeno Flash 10.1 o successivo </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Per la funzione di fallback su software, Flash 15 e versioni successive </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Browser e <span class="codeph"> wmode</span> impostazioni </td> 
   <td colname="col2"> <p><b>Il Flash 15</b>, impostato <span class="codeph"> wmode=opaco</span> in modo da poter utilizzare le sovrapposizioni HTML. </p> <p>I seguenti browser non supportano attualmente l'accelerazione hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox su Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome prima del 26° giorno e qualsiasi versione di Chrome su Windows XP e Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (tutte le versioni) </li> 
     </ul>Altre combinazioni browser/sistema operativo potrebbero impedire l'accesso all'accelerazione hardware. In questi scenari, <span class="codeph"> StageVideo</span> si basa sul software, con un impatto negativo sulle prestazioni. </p> <p><b>Il Flash 14 e versioni precedenti</b>, se il browser non supporta l'accelerazione hardware, il lettore di Flash può eseguire il rendering direttamente nella GPU, ma imposta <span class="codeph"> wmode=direct</span> per abilitare questo rendering. <p>Suggerimento: potrebbe essere necessario aggiornare i driver GPU precedenti al 2009, in quanto potrebbero non essere supportati per l'accelerazione hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Oggetto NetStream </td> 
   <td colname="col2">Il <span class="codeph"> StageVideoEvent.RENDER_STATE</span> non viene inviato a meno che non si alleghi un <span class="codeph"> NetStream</span> oggetto al <span class="codeph"> StageVideo</span> oggetto. </td> 
  </tr> 
 </tbody> 
</table>
