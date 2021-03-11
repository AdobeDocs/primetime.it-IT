---
title: Funzionalità del dispositivo necessarie per riprodurre contenuti protetti
description: Funzionalità del dispositivo necessarie per riprodurre contenuti protetti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Funzionalità del dispositivo necessarie per riprodurre contenuto protetto {#device-capabilities-required-to-play-protected-content}

Le funzionalità del dispositivo richieste specificano le funzionalità hardware necessarie per accedere ai contenuti. Le informazioni sulle funzionalità hardware sono disponibili per i dispositivi che utilizzano il kit di supporto.

I seguenti attributi possono identificare le funzionalità del dispositivo:

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Attributo</b> </td> 
   <td><b>Valori supportati</b> </td> 
   <td><b>Criteri di corrispondenza</b> </td> 
   <td><b>Descrizione</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Bus accessibile non utente </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Corrispondenza esatta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Se true, il dispositivo non deve avere un bus accessibile all'utente. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Radice hardware di affidabilità </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" o "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Corrispondenza esatta </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Se true, il dispositivo deve avere una radice hardware di attendibilità. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client Adobe Primetime DRM versione 2.0.2 e successive. Il comportamento dei client meno recenti dipende dalla versione client minima supportata dal server licenze.
>
>Vedere [Versione minima del client](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).

