---
title: Panoramica
description: Panoramica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Generatore di licenze DRM {#license-generator}

Utilizzare [!DNL AdobeLicenseGenerator.jar] per generare le licenze senza richiedere al client di inviare una richiesta di licenza a un server. Puoi quindi incorporare nel contenuto una licenza pregenerata o distribuire la licenza al client tramite altri meccanismi, ad esempio un semplice server web HTTP.

## Utilizzo della riga di comando del generatore di licenze {#license-generator-command-line-usage}

**Generare una licenza:**

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

  Puoi recuperare questo file da contenuto protetto con `-d -m` in Media Packager.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, il Generatore di licenze DRM cerca <span class="filepath"> flashaccesstools.properties</span> nella directory di lavoro corrente. </p> <p>Nota: le opzioni specificate nella riga di comando hanno la precedenza su quelle specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Visualizza informazioni su una licenza già generata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licenza foglia e salva l'output in un file specificato. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nome-file-metadati</span> </td> 
   <td colname="2" class="- topic/entry "> Specifica i metadati di contenuto per i quali è necessario generare una licenza. Questa opzione è necessaria per generare una licenza. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e il <span class="codeph"> -o</span> non è stato impostato, si verifica un errore. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, è possibile sovrascriverlo senza che venga richiesto. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se i metadati includono più criteri DRM, è possibile specificare il numero di criteri DRM che è possibile utilizzare per generare una licenza. </p> <p>Se non si specifica il numero di criteri DRM, viene applicato automaticamente il primo criterio DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificato destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licenza per un destinatario specificato. È possibile utilizzare un certificato di dispositivo o dominio e specificare più certificati <span class="+ topic/ph pr-d/codeph codeph"> -r </span>opzioni per creare una licenza per più destinatari. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licenza radice e salva l'output in un file specificato. </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà del file di configurazione {#configuration-file-properties}

Prima di eseguire License Generator, è necessario specificare i valori per le proprietà License Generator nel file di configurazione.

>[!NOTE]
>
>Per nomi di proprietà che includono *n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

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
   <td colname="2" class="- topic/entry "> <p>Imposta la versione minima del client attualmente supportata. Se non si imposta questa proprietà, tutte le versioni vengono supportate automaticamente per impostazione predefinita. </p> <p>È possibile impostare questo valore per controllare in che modo i client meno recenti rispondono ai requisiti di licenza non supportati. Specifica <span class="codeph"> x</span> (per Adobe Primetime DRM x.0) dove <span class="codeph"> x</span> rappresenta un numero di versione principale. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificato server chiavi, un certificato server licenze rilasciato da un Adobe utilizzato dal server chiavi. Questo certificato viene applicato solo se i criteri di metadati/DRM indicano che è necessario un server chiavi per la distribuzione di chiavi ai dispositivi iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> Il file PKCS12 che include le credenziali del server licenze per la firma delle licenze. Questa proprietà deve fare riferimento a un file .pfx che include un certificato e una chiave privata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La password che protegge il file specificato con <span class="+ topic/ph pr-d/codeph codeph"> licegen.sign.certfile</span> opzione. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se si generano licenze associate a dominio, è necessario specificare uno o più certificati CA di dominio per indicare le autorità di dominio che l'autorità emittente delle licenze può considerare attendibili. </p> <p>Se il destinatario della licenza è un certificato di dominio non rilasciato da una delle CA di dominio specificate, non è possibile generare una licenza. Questa proprietà specifica un <span class="filepath"> cer</span> file che include il certificato nel formato PEM o DER. <span class="codeph">n</span> deve aumentare in modo monotonico, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File PKCS12 opzionale che include credenziali aggiuntive del server licenze per decrittografare il CEK nei metadati e nei criteri DRM. È possibile configurare credenziali aggiuntive se in precedenza il contenuto è stato compilato con un certificato del server licenze diverso dalle credenziali specificate con <span class="codeph"> licegen.sign.certfile</span>. Questa proprietà deve fare riferimento a un <span class="filepath"> .pfx</span> che include un certificato e una chiave privata. <span class="codeph">n</span> deve aumentare in modo monotonico, a partire da 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>La password viene applicata per proteggere il file specificato con<span class="+ topic/ph pr-d/codeph codeph"> licegen.keys.asymmetric.licenseServerCredential.n</span> proprietà. </p> </td> 
  </tr> 
 </tbody> 
</table>
