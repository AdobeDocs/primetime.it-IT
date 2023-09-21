---
description: Controlla le restrizioni e i requisiti per flussi e playlist (manifesti).
title: Requisiti del contenuto e del manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Requisiti del contenuto e del manifesto{#content-and-manifest-requirements}

Controlla le restrizioni e i requisiti per flussi e playlist (manifesti).

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Durata del segmento di contenuto </td> 
   <td colname="col2"> La durata di un segmento non deve superare la durata target specificata nel file manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Requisito contenuto </td> 
   <td colname="col2"> Ogni segmento TS deve iniziare con un keyframe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Contenuto HLS </td> 
   <td colname="col2"> <p>Tenere presente quanto segue: 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">Audio AAC-SSR non supportato. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">I codec audio AC3 e Enhanced AC3 non sono supportati. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">Flussi HLS con discontinuità, ma non sono supportati marcatori di discontinuità. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live non supporta il rollover della marca temporale. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">Gli annunci nella finestra DVR dei flussi HLS Live non vengono risolti. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">L'intervallo di byte non è supportato con contenuto crittografato AES-128. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Contenuto tratteggio </td> 
   <td colname="col2"> <p>Tenere presente quanto segue: 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">Per flussi live: è supportato il profilo live con tipo dinamico. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">Per flussi VOD: è supportato il profilo live con tipo statico. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">Per i flussi VOD - Il profilo on-demand non è certificato per i flussi di lavoro degli annunci. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">La riproduzione di flussi DASH con più periodi non è supportata. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">Sono supportati i sottotitoli incorporati (608/708), segnalati tramite il tag Accessibilità. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">I file VTT frammentati/segmentati non sono supportati. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">I flussi con tag personalizzati in banda non sono certificati. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>
