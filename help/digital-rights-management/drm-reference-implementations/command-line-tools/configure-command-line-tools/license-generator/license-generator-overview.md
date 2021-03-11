---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Generatore di licenze DRM {#license-generator}

Utilizza [!DNL AdobeLicenseGenerator.jar] per generare le licenze senza richiedere al client di inviare una richiesta di licenza a un server. È quindi possibile incorporare una licenza pregenerata nel contenuto o distribuire la licenza al client tramite altri meccanismi, ad esempio un semplice server web HTTP.

## Uso della riga di comando di License Generator {#license-generator-command-line-usage}

**Genera una licenza:**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata` - Include i metadati DRM di Adobe Primetime.

   È possibile recuperare questo file dal contenuto protetto con le opzioni `-d -m` in Media Packager.

**Visualizza una licenza generata in precedenza:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - Contiene una licenza Adobe Primetime DRM generata dal Generatore di licenze.

**Tabella 6: Opzioni**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c file di configurazione</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e il percorso del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, il Generatore di licenze DRM cerca <span class="filepath"> flashaccesstools.properties</span> nella directory di lavoro corrente. </p> <p>Nota:  Le opzioni specificate nella riga di comando hanno la precedenza sulle opzioni specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> file di licenza</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Visualizza informazioni su una licenza già generata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-nomefile foglia</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licenza foglia e salva l'output in un file specificato. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-nomefile</span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati del contenuto per i quali è necessario generare una licenza. Questa opzione è necessaria per generare una licenza. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o</span> non è stato impostato, si verifica un errore. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, puoi sovrascriverlo senza che venga richiesto di farlo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se i metadati includono più criteri DRM, è possibile specificare il numero di criteri DRM che è possibile utilizzare per generare una licenza. </p> <p>Se non si specifica il numero di criteri DRM, il primo criterio DRM viene applicato automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r Certificato del destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licenza per un destinatario specificato. Puoi utilizzare un certificato di dispositivo o dominio e specificare più opzioni <span class="+ topic/ph pr-d/codeph codeph"> -r </span>per creare una licenza per più destinatari. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-nomefile</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licenza root e salva l'output in un file specificato. </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà del file di configurazione {#configuration-file-properties}

Prima di eseguire License Generator, è necessario specificare i valori per le proprietà di License Generator nel file di configurazione.

>[!NOTE]
>
>Per i nomi di proprietà che includono *n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

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
   <td colname="2" class="- topic/entry "> <p>Imposta la versione client minima attualmente supportata. Se non si imposta questa proprietà, tutte le versioni sono supportate automaticamente per impostazione predefinita. </p> <p>È possibile impostare questo valore per controllare in che modo i client meno recenti rispondono ai requisiti di licenza che non supportano. Specifica <span class="codeph"> x</span> (per Adobe Primetime DRM x.0) in cui <span class="codeph"> x</span> rappresenta un numero di rilascio principale. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificato del server chiavi, certificato del server licenze rilasciato da Adobe utilizzato dal server chiavi. Questo certificato viene applicato solo se il criterio metadati/DRM indica che è necessario un server chiavi per la consegna delle chiavi ai dispositivi iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> File PKCS12 che include le credenziali del server licenze per la firma delle licenze. Questa proprietà deve fare riferimento a un file .pfx che include un certificato e una chiave privata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La password che protegge il file specificato con l'opzione <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span>. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se si generano licenze con associazione a dominio, è necessario specificare uno o più certificati CA di dominio per indicare le autorità di dominio considerate attendibili dall'emittente. </p> <p>Se il destinatario della licenza è un certificato di dominio non rilasciato da una delle CA di dominio specificate, non è possibile generare una licenza. Questa proprietà specifica un file <span class="filepath"> .cer</span> che include il certificato in formato PEM o DER. <span class="codeph"></span> Non deve aumentare monotonicamente, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File PKCS12 facoltativo che include credenziali aggiuntive per il server licenze per la decrittografia della CEK nei metadati e nei criteri DRM. È possibile configurare le credenziali aggiuntive se il contenuto è stato precedentemente incluso in un pacchetto con un certificato License Server diverso dalle credenziali specificate con <span class="codeph"> licensegen.sign.certfile</span>. Questa proprietà deve fare riferimento a un file <span class="filepath"> .pfx</span> che include un certificato e una chiave privata. <span class="codeph"></span> Non deve aumentare monotonicamente, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>La password viene applicata per proteggere il file specificato con la proprietà<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>