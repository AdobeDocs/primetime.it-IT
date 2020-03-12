---
seo-title: Proprietà file di configurazione
title: Proprietà file di configurazione
uuid: 13e158a6-c447-4e5e-884d-03fb4835c120
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Proprietà file di configurazione {#configuration-file-properties}

Prima di eseguire License Generator, specificate i valori per le proprietà License Generator. Il file di configurazione specifica le seguenti proprietà. Per i nomi di proprietà che includono *n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

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
   <td colname="2" class="- topic/entry "> Impostate la versione client minima supportata. Se non è impostato, per impostazione predefinita sono supportate tutte le versioni. Impostate questo valore per controllare in che modo i client meno recenti rispondono ai requisiti di licenza che non supportano. Specificate x (per Adobe Access x.0) dove x è il numero di rilascio principale. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificato server chiavi (un certificato server licenze emesso da Adobe e utilizzato dal server chiavi). Questo certificato viene utilizzato solo se i metadati/criteri indicano che per la consegna delle chiavi ai dispositivi iOS è necessario un server chiavi. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> Il file PKCS12 contenente le credenziali del server licenze per le licenze di firma. Questa proprietà deve fare riferimento a un file .pfx contenente un certificato e una chiave privata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La password utilizzata per proteggere il file specificato da <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Se si generano licenze con binding di dominio, è necessario specificare uno o più certificati CA di dominio per indicare le autorità di dominio attendibili dall'emittente della licenza. Se il destinatario della licenza è un certificato di dominio, che non è stato rilasciato da una delle CA di dominio specificate, non è possibile generare una licenza. Questa proprietà specifica un file cer che contiene solo il certificato (il formato PEM o DER è accettabile). n deve essere in aumento monotonico, a partire da 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymMetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File PKCS12 facoltativo contenente credenziali aggiuntive per la decrittografia di CEK nei metadati e nei criteri. È possibile configurare credenziali aggiuntive se il contenuto è stato precedentemente incluso in un pacchetto con un certificato del server licenze diverso da quello specificato da <span class="codeph"> licensegen.sign.certfile</span>. Questa proprietà deve fare riferimento a un file <span class="filepath"> .pfx</span> contenente un certificato e una chiave privata. n deve essere in aumento monotonico, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymMetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">La password utilizzata per proteggere il file specificato da: <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymMetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

