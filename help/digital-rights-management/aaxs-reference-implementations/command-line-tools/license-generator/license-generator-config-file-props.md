---
title: Proprietà del file di configurazione
description: Proprietà del file di configurazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Proprietà del file di configurazione {#configuration-file-properties}

Prima di eseguire License Generator, specificare i valori per le proprietà di License Generator. Il file di configurazione specifica le seguenti proprietà. Per i nomi di proprietà che includono *n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Proprietà </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> Imposta la versione client minima supportata. Se non è impostato, per impostazione predefinita sono supportate tutte le versioni. Imposta questo valore per controllare in che modo i client meno recenti rispondono ai requisiti di licenza che non supportano. Specifica x (ad Adobe Access x.0) dove x è il numero di rilascio principale. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificato del server chiavi (certificato del server licenze rilasciato da un Adobe utilizzato dal server chiavi). Questo certificato viene utilizzato solo se i metadati/criteri indicano che è necessario un server chiavi per la consegna delle chiavi ai dispositivi iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> File PKCS12 contenente le credenziali del server licenze per la firma delle licenze. Questa proprietà deve fare riferimento a un file .pfx contenente un certificato e una chiave privata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">Password utilizzata per proteggere il file specificato da <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Se si generano licenze con associazione a dominio, è necessario specificare uno o più certificati CA di dominio per indicare le autorità di dominio considerate attendibili dall'emittente della licenza. Se il destinatario della licenza è un certificato di dominio non rilasciato da una delle CA di dominio specificate, non è possibile generare una licenza. Questa proprietà specifica un file .cer contenente solo il certificato (il formato PEM o DER è accettabile). n deve aumentare monotonicamente, a partire da 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File PKCS12 opzionale contenente credenziali aggiuntive per il server licenze per la decrittografia della CEK nei metadati e nei criteri. È possibile configurare credenziali aggiuntive se il contenuto è stato precedentemente incluso con un certificato License Server diverso da quello specificato da <span class="codeph"> licensegen.sign.certfile</span>. Questa proprietà deve fare riferimento a un file <span class="filepath"> .pfx</span> contenente un certificato e una chiave privata. n deve aumentare monotonicamente, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">Password utilizzata per proteggere il file specificato da: <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

