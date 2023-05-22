---
title: Funzionalità del dispositivo necessarie per riprodurre contenuti protetti
description: Funzionalità del dispositivo necessarie per riprodurre contenuti protetti
copied-description: true
exl-id: 540fbb53-ec1a-43be-b51b-9937ed31e384
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Funzionalità del dispositivo necessarie per riprodurre contenuti protetti {#device-capabilities-required-to-play-protected-content}

Le funzionalità del dispositivo richieste specificano le funzionalità hardware necessarie per accedere al contenuto. Le informazioni sulle funzionalità hardware sono disponibili per i dispositivi che utilizzano il kit di portabilità.

I seguenti attributi possono identificare le funzionalità del dispositivo:

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Attributo</b> </td> 
   <td><b>Valori supportati</b> </td> 
   <td><b>Corrispondenza criteri</b> </td> 
   <td><b>Descrizione</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Bus non accessibile all'utente </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Corrispondenza esatta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Se true, il dispositivo non deve disporre di un bus accessibile all'utente. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Directory principale hardware attendibile </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Corrispondenza esatta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Se true, il dispositivo deve avere una radice hardware di attendibilità. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client Adobe Primetime DRM versione 2.0.2 e successive. Il comportamento sui client meno recenti dipende dalla versione minima del client supportata dal server licenze.
>
>Consulta [Versione client minima](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
