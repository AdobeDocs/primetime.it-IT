---
title: File delle proprietà del server licenze
description: File delle proprietà del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# File delle proprietà del server licenze {#license-server-properties-file}

Utilizza il file [!DNL flashaccess-refimpl.properties] per configurare il componente Server licenze per l’implementazione di riferimento. Come minimo, assicurarsi di configurare le proprietà relative alle credenziali di trasporto e alle credenziali del server licenze. Le posizioni dei file delle credenziali devono essere specificate rispetto alla directory specificata dalla proprietà `config.resourcesDirectory` . Questo file contiene anche diverse proprietà relative al contenuto del pacchetto: queste proprietà vengono utilizzate solo per la conversione dei metadati Flash Media Rights Management Server 1.x. Se modifichi uno dei valori in questo file di proprietà, è necessario riavviare il server licenze per rendere effettive le modifiche.

Per supportare la generazione di licenze per la distribuzione di chiavi remote ai client iOS in Adobe Access, è necessario specificare il certificato del server chiavi in [!DNL flashaccess-refimpl.properties].

In Access Adobe sono state aggiunte le seguenti proprietà:

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
   <td colname="2" class="- topic/entry "> Certificato del server licenze di Key Server, rilasciato da Adobe. Questo certificato viene utilizzato per generare licenze per dispositivi iOS, quando i metadati indicano che è necessario un server chiavi. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias del certificato del server licenze rilasciato dall'Adobe memorizzato in HSM. Quando HSM è abilitato, utilizza questa proprietà invece di <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>

