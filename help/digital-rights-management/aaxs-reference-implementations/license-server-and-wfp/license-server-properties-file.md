---
seo-title: File delle proprietà del server licenze
title: File delle proprietà del server licenze
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# File delle proprietà del server licenze {#license-server-properties-file}

Utilizzate il [!DNL flashaccess-refimpl.properties] file per configurare il componente Server licenze dell&#39;implementazione di riferimento. Come minimo, assicurarsi di configurare le proprietà relative alle credenziali di trasporto e alle credenziali del server licenze. I percorsi dei file delle credenziali devono essere specificati rispetto alla directory specificata dalla `config.resourcesDirectory` proprietà. Questo file contiene anche diverse proprietà relative alla creazione di pacchetti di contenuto: queste proprietà vengono utilizzate solo per la conversione di metadati Flash Media Rights Management Server 1.x. Se modificate uno dei valori di questo file di proprietà, è necessario riavviare il server licenze per rendere effettive le modifiche.

Per supportare la generazione di licenze per la consegna di chiavi remote ai client iOS in Adobe Access, è necessario specificare il certificato Server chiavi in [!DNL flashaccess-refimpl.properties].

In Adobe Access sono state aggiunte le seguenti proprietà:

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
   <td colname="2" class="- topic/entry "> Certificato server licenze del server chiavi, rilasciato da Adobe. Questo certificato viene utilizzato per generare licenze per i dispositivi iOS, quando i metadati indicano che è necessario un server chiavi. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias del certificato del server delle licenze emesso da Adobe dal server delle chiavi memorizzato in HSM. Quando HSM è abilitato, utilizzare questa proprietà invece di <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>

