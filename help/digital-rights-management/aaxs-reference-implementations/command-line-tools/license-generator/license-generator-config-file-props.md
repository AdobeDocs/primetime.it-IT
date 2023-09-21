---
title: Proprietà file di configurazione
description: Proprietà file di configurazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Proprietà file di configurazione {#configuration-file-properties}

Prima di eseguire License Generator, specificare i valori per le proprietà License Generator. Il file di configurazione specifica le seguenti proprietà. Per nomi di proprietà che includono *n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Proprietà </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> Imposta la versione client minima supportata. Se non è impostato, per impostazione predefinita sono supportate tutte le versioni. Impostare questo valore per controllare il modo in cui i client meno recenti rispondono ai requisiti di licenza non supportati. Specifica x (ad Adobe Access x.0) dove x è il numero della versione principale. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificato server chiavi (certificato server licenze rilasciato da un Adobe utilizzato dal server chiavi). Questo certificato viene utilizzato solo se i metadati o i criteri indicano che è necessario un server chiavi per la consegna delle chiavi ai dispositivi iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> Il file PKCS12 contenente le credenziali del server licenze per la firma delle licenze. Questa proprietà deve fare riferimento a un file .pfx contenente un certificato e una chiave privata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">Password utilizzata per proteggere il file specificato da <span class="+ topic/ph pr-d/codeph codeph"> licegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> In caso di generazione di licenze con limiti di dominio, è necessario specificare uno o più certificati CA di dominio per indicare le autorità di dominio considerate attendibili da questo emittente di licenze. Se il destinatario della licenza è un certificato di dominio non rilasciato da una delle CA di dominio specificate, non è possibile generare una licenza. Questa proprietà specifica un file con estensione cer contenente solo il certificato (è possibile utilizzare il formato PEM o DER). n deve aumentare in modo monotono, a partire da 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File PKCS12 opzionale contenente credenziali aggiuntive del server licenze per decrittografare il CEK nei metadati e nei criteri. È possibile configurare credenziali aggiuntive se il contenuto è stato precedentemente compilato con un certificato del server licenze diverso da quello specificato da <span class="codeph"> licegen.sign.certfile</span>. Questa proprietà deve fare riferimento a un <span class="filepath"> .pfx</span> file contenente un certificato e una chiave privata. n deve aumentare in modo monotono, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">Password utilizzata per proteggere il file specificato da: <p><span class="+ topic/ph pr-d/codeph codeph"> licegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
