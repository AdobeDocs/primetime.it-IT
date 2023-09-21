---
title: Proprietà di consegna della chiave remota (iOS)
description: Proprietà di consegna della chiave remota (iOS)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Proprietà di consegna della chiave remota (iOS){#remote-key-delivery-properties-ios}

Per supportare la generazione di licenze per la consegna di chiavi remote a un client iOS in Adobe Primetime DRM, è necessario specificare il certificato del server chiavi in `flashaccess-refimpl.properties` file.

In Primetime DRM sono state aggiunte le seguenti proprietà:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Proprietà </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Certificato del server licenze del server chiavi rilasciato da Adobe. </p> <p>Questo certificato genera licenze per i dispositivi iOS quando i metadati indicano che è necessario un server chiavi. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Alias del certificato del server licenze rilasciato da un Adobe di un server chiavi memorizzato in HSM. </p> <p>Quando abiliti HSM, puoi applicare questa proprietà invece del <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> proprietà. </p> </td> 
  </tr> 
 </tbody> 
</table>
