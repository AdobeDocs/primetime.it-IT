---
title: Proprietà del file di configurazione
description: Proprietà del file di configurazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare il contenuto video. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare l'audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se crittografare i dati di script in FLV. <i class="+ topic/ph hi-d/i ">I tag dati </i> onMetaDatae  <i class="+ topic/ph hi-d/i "></i> onXMPscript non vengono mai crittografati, anche se questa opzione è abilitata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica il livello di crittografia video. Un valore di high viene utilizzato per cifrare tutti i contenuti video, mentre valori di medium e Low vengono utilizzati per cifrare parti del contenuto video per file F4V contenenti contenuto H.264. </p> <p class="- topic/p ">value = <span class="codeph"> high | media | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsNon crittografato</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il valore è maggiore di 0, il numero specificato di secondi di contenuto all’inizio del file non verrà crittografato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File del certificato del server di licenza utilizzato per crittografare la chiave. La proprietà <span class="codeph"> encrypt.keys.asymmetric.certfile</span> specifica un file che contiene solo il certificato (il formato PEM o DER è accettabile). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Questa proprietà viene utilizzata ripetutamente per creare un elenco di criteri da applicare al contenuto. <span class="codeph"> </span> è un numero intero il cui valore è maggiore o uguale a 1. Per impostazione predefinita, il client utilizza la prima istanza. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server licenze. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certificato di trasporto per il server licenze. Questa proprietà specifica un file <span class="filepath"> .cer</span> contenente solo il certificato (è accettabile il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il file PKCS12 contenente le credenziali del packager per la firma del contenuto. Il file <span class="codeph"> encrypt.sign.certfile</span> deve fare riferimento a un file <span class="filepath"> .pfx</span> contenente un certificato e una chiave privata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Password utilizzata per proteggere il file specificato da <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Imposta la versione minima del server necessaria per rilasciare licenze per il contenuto in fase di creazione del pacchetto. Specifica x (Adobe Access x.0) dove x = il numero di rilascio principale. I server precedenti ad Adobe Access 3.0 non supportano questa impostazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un criterio <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, è necessario fornire il certificato di trasporto del dominio. </p> <p class="- topic/p ">Questa proprietà specifica un file contenente solo il certificato (è accettabile il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la chiave di licenza. Se non viene specificata alcuna chiave, la chiave verrà generata in modo casuale. Quando la rotazione delle chiavi non è abilitata, si tratta della chiave utilizzata per crittografare il contenuto. </p> <p class="- topic/p ">Quando la rotazione dei tasti è attivata, questo tasto viene utilizzato per proteggere i tasti di rotazione. La chiave deve avere una lunghezza di 16 byte e deve essere specificata come valore esadecimale. Lo spazio vuoto tra i valori esadecimali è facoltativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rot.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica se la rotazione delle chiavi è abilitata. Se è impostato su false (impostazione predefinita), la rotazione della chiave è disabilitata e il CEK principale verrà utilizzato per crittografare tutti i campioni nel contenuto. </p> <p class="- topic/p ">Se è impostato su true, la rotazione delle chiavi verrà abilitata e sarà possibile utilizzare chiavi diverse per cifrare parti del contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rot.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequenza di chiavi ruotate utilizzate per cifrare il contenuto quando la rotazione delle chiavi è abilitata. Se non viene specificata alcuna chiave, le chiavi verranno generate in modo casuale. Le chiavi devono avere una lunghezza di 16 byte e devono essere specificate come valori esadecimali. </p> <p class="- topic/p ">Lo spazio vuoto tra i valori esadecimali è facoltativo. <i class="+ topic/ph hi-d/i "></i> deve aumentare monotonicamente, a partire da 1. Quando vengono specificate più chiavi, le chiavi vengono sottoposte a ciclo continuo nell’ordine indicato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotv.Interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica l’intervallo (in secondi) in cui verrà utilizzata una chiave di rotazione per crittografare gli esempi di contenuto. </p> <p class="- topic/p ">Dopo aver crittografato questo periodo di tempo nel contenuto, verrà utilizzata la chiave di rotazione successiva. Se la rotazione dei tasti è attivata e non viene specificato alcun intervallo, i tasti vengono ruotati ogni 15 minuti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se true, non esiste un server licenze da cui è possibile ottenere le licenze. Le licenze devono essere incorporate o ottenute fuori banda. Il valore predefinito è false se non è specificato. Supportato solo in Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>

