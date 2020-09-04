---
seo-title: Panoramica
title: Panoramica
uuid: 857390be-dd14-46c0-b8f7-2bc661c515d4
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Generatore di licenze DRM {#license-generator}

Utilizzare [!DNL AdobeLicenseGenerator.jar] per generare le licenze senza richiedere al client di inviare una richiesta di licenza a un server. Potete quindi incorporare una licenza pregenerata nel contenuto o distribuirla al client tramite altri meccanismi, ad esempio un semplice server Web HTTP.

## Utilizzo della riga di comando di License Generator {#license-generator-command-line-usage}

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

* `metadata` - Include i metadati DRM  Adobe Primetime.

   Potete recuperare questo file dal contenuto protetto con le `-d -m` opzioni in Media Packager.

**Visualizzare una licenza generata in precedenza:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - Contiene una licenza Adobe Primetime DRM  generata dal Generatore di licenze.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, DRM License Generator cerca <span class="filepath"> flashaccesstools.properties</span> nella directory di lavoro corrente. </p> <p>Nota:  Le opzioni specificate nella riga di comando hanno la precedenza rispetto alle opzioni specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
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
   <td colname="2" class="- topic/entry ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e il <span class="codeph"> -o</span> non è stato impostato, si verifica un errore. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, potete sovrascriverlo senza che venga richiesto. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se i metadati includono più criteri DRM, potete specificare il numero di criteri DRM che potete utilizzare per generare una licenza. </p> <p>Se non si specifica il numero di criteri DRM, viene applicato automaticamente il primo criterio DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificato destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licenza per un destinatario specificato. Potete utilizzare un certificato di dispositivo o di dominio e specificare più <span class="+ topic/ph pr-d/codeph codeph"> - </span>opzioni per creare una licenza per più destinatari. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licenza radice e salva l'output in un file specificato. </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà del file di configurazione {#configuration-file-properties}

Prima di eseguire License Generator, è necessario specificare i valori per le proprietà License Generator nel file di configurazione.

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
   <td colname="2" class="- topic/entry "> <p>Imposta la versione client minima attualmente supportata. Se non si imposta questa proprietà, per impostazione predefinita vengono automaticamente supportate tutte le versioni. </p> <p>Potete impostare questo valore per controllare in che modo i client meno recenti rispondono ai requisiti di licenza che non supportano. Specificate <span class="codeph"> x</span> (per  Adobe Primetime DRM x.0) dove <span class="codeph"> x</span> rappresenta un numero di rilascio principale. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificato server chiavi, che è un certificato del server licenze emesso  Adobe utilizzato dal server chiavi. Questo certificato viene applicato solo se il criterio metadati/DRM indica che per la consegna delle chiavi ai dispositivi iOS è necessario un server chiavi. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> Il file PKCS12 che include le credenziali del server licenze per le licenze di firma. Questa proprietà deve fare riferimento a un file .pfx che include un certificato e una chiave privata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La password che protegge il file specificato con l'opzione <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> . </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se si generano licenze con binding di dominio, è necessario specificare uno o più certificati CA di dominio per indicare le autorità di dominio considerate attendibili dall'emittente della licenza. </p> <p>Se il destinatario della licenza è un certificato di dominio, che non è stato rilasciato da una delle CA di dominio specificate, non è possibile generare una licenza. Questa proprietà specifica un file <span class="filepath"> .cer</span> che include il certificato in formato PEM o DER. <span class="codeph">n</span> deve aumentare monotonicamente, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File PKCS12 opzionale che include credenziali aggiuntive per il server licenze per decrittografare CEK nei metadati e nei criteri DRM. È possibile configurare credenziali aggiuntive se il contenuto è stato precedentemente incluso in un pacchetto con un certificato del server licenze diverso da quelle specificate con <span class="codeph"> licensegen.sign.certfile</span>. Questa proprietà deve fare riferimento a un file <span class="filepath"> .pfx</span> che include un certificato e una chiave privata. <span class="codeph">n</span> deve aumentare monotonicamente, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>La password viene applicata per proteggere il file specificato con la<span class="+ topic/ph pr-d/codeph codeph"> proprietà licensegen.keys.asymMetric.licenseServerCredential.n</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>