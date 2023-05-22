---
title: Proprietà del file di configurazione
description: Proprietà del file di configurazione
copied-description: true
exl-id: eec6a53d-d831-4ec4-a90c-8b3e7997f330
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Proprietà del file di configurazione {#configuration-file-properties}

Prima di eseguire Media Packager, specificare i valori per le proprietà di Media Packager. Il file di configurazione specifica le seguenti proprietà. Per i nomi di proprietà che includono* n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Proprietà </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare il contenuto video. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare l'audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se crittografare i dati script in FLV. <i class="+ topic/ph hi-d/i ">onMetaData</i> e <i class="+ topic/ph hi-d/i ">onXMP</i> i tag di dati script non vengono mai crittografati, anche se questa opzione è abilitata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica il livello di crittografia del video. Il valore high viene utilizzato per crittografare tutto il contenuto video, mentre i valori medium e low vengono utilizzati per crittografare parti del contenuto video per file F4V contenenti contenuto H.264. </p> <p class="- topic/p ">value = <span class="codeph"> alta | medio | bassa</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il valore è maggiore di 0, il numero specificato di secondi di contenuto all'inizio del file non verrà crittografato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File del certificato del server licenze utilizzato per crittografare la chiave. Il <span class="codeph"> encrypt.keys.asymmetric.certfile</span> specifica un file contenente solo il certificato (è possibile utilizzare il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Questa proprietà viene utilizzata ripetutamente per creare un elenco di criteri da applicare al contenuto. <span class="codeph"> n</span> è un numero intero il cui valore è maggiore o uguale a 1. Per impostazione predefinita, il client utilizzerà la prima istanza. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server licenze. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certificato di trasporto per il server licenze. Questa proprietà specifica un <span class="filepath"> cer</span> file contenente solo il certificato (è accettabile il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il file PKCS12 contenente le credenziali del packager per la firma del contenuto. Il <span class="codeph"> encrypt.sign.certfile</span> deve fare riferimento a un <span class="filepath"> .pfx</span> file contenente un certificato e una chiave privata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Password utilizzata per proteggere il file specificato da <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Imposta la versione minima del server necessaria per rilasciare le licenze per il contenuto da includere nel pacchetto. Specifica x (Adobe Access x.0) dove x = il numero della versione principale. I server precedenti ad Adobe Access 3.0 non supportano questa impostazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se una policy <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, è necessario fornire il certificato di trasporto del dominio. </p> <p class="- topic/p ">Questa proprietà specifica un file che contiene solo il certificato (è possibile utilizzare il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il codice di licenza. Se non viene specificata alcuna chiave, verrà generata in modo casuale. Quando la rotazione delle chiavi non è abilitata, questa è la chiave utilizzata per crittografare il contenuto. </p> <p class="- topic/p ">Quando è abilitata la rotazione delle chiavi, questa chiave viene utilizzata per proteggere le chiavi di rotazione. La chiave deve essere lunga 16 byte e specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica se la rotazione delle chiavi è abilitata. Se è impostato su false (impostazione predefinita), la rotazione delle chiavi è disabilitata e il codice master CEK verrà utilizzato per crittografare tutti i campioni nel contenuto. </p> <p class="- topic/p ">Se è impostato su true, verrà attivata la rotazione delle chiavi e sarà possibile utilizzare chiavi diverse per crittografare parti del contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequenza di chiavi ruotate utilizzate per crittografare il contenuto quando la rotazione delle chiavi è abilitata. Se non viene specificata alcuna chiave, le chiavi verranno generate in modo casuale. Le chiavi devono essere lunghe 16 byte e specificate come valori esadecimali. </p> <p class="- topic/p ">Lo spazio vuoto tra i valori esadecimali è facoltativo. <i class="+ topic/ph hi-d/i ">n</i> deve aumentare in modo monotono, a partire da 1. Se sono specificati più tasti, i tasti vengono spostati nell'ordine indicato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica l'intervallo (in secondi) durante il quale verrà utilizzata una chiave di rotazione per crittografare i campioni di contenuto. </p> <p class="- topic/p ">Dopo che questo periodo di tempo nel contenuto è stato crittografato, verrà utilizzata la chiave di rotazione successiva. Se la rotazione delle chiavi è attivata e non è specificato alcun intervallo, le chiavi verranno ruotate ogni 15 minuti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se true, non è disponibile alcun server licenze da cui è possibile ottenere le licenze. Le licenze devono essere incorporate o ottenute fuori banda. Se non specificato, il valore predefinito è false. Supportato solo in Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
