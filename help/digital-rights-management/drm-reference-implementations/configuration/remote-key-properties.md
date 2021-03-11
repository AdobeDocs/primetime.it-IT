---
title: Proprietà di consegna chiavi remote (iOS)
description: Proprietà di consegna chiavi remote (iOS)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Proprietà di consegna chiavi remote (iOS){#remote-key-delivery-properties-ios}

Per supportare la generazione di licenze per la consegna di chiavi remote a un client iOS in Adobe Primetime DRM , devi specificare il certificato del server chiavi nel file `flashaccess-refimpl.properties` .

Le seguenti proprietà sono state aggiunte in Primetime DRM :

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
   <td colname="2" class="- topic/entry "> <p>Certificato server licenze del server chiavi rilasciato da Adobe. </p> <p>Questo certificato genera licenze per dispositivi iOS quando i metadati indicano che è necessario un server chiavi. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>L'alias di un certificato License Server rilasciato da un Adobe del server che è memorizzato in HSM. </p> <p>Quando abiliti HSM, puoi applicare questa proprietà invece della proprietà <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

