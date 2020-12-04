---
description: 'null'
seo-description: 'null'
seo-title: Proprietà di consegna chiave remota (iOS)
title: Proprietà di consegna chiave remota (iOS)
uuid: 17e1b756-d106-47a7-99ae-641190693870
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Proprietà di consegna chiave remota (iOS){#remote-key-delivery-properties-ios}

Per supportare la generazione di licenze per la consegna di chiavi remote a un client iOS in  Adobe Primetime DRM, è necessario specificare il certificato Server chiavi nel file `flashaccess-refimpl.properties`.

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
   <td colname="2" class="- topic/entry "> <p>Certificato server licenze del server chiavi emesso dal Adobe . </p> <p>Questo certificato genera licenze per i dispositivi iOS quando i metadati indicano che è necessario un server chiavi. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>L'alias del certificato del server licenze rilasciato  Adobe da un server chiavi memorizzato in HSM. </p> <p>Quando si abilita HSM, è possibile applicare questa proprietà invece della proprietà <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

