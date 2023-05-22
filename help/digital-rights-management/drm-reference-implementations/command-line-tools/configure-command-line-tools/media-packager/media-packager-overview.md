---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 866b3147-c28b-41b0-8653-06ba867354c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# DRM Media Packager {#media-packager}

Utilizzare Media Packager ( [!DNL AdobePackager.jar]) per specificare una policy DRM da applicare al contenuto e per specificare quale parte del contenuto crittografare. Ad esempio, è possibile specificare che il packager crittografi i dati video, ma non i dati audio.

Prima dell’esecuzione [!DNL AdobePackager.jar], è necessario impostare le proprietà nella sezione Proprietà di Media Packager del file di configurazione.

>[!NOTE]
>
>Puoi anche specificare tutte le proprietà di Media Packager dalla riga di comando.

## Utilizzo della riga di comando di Media Packager {#media-packager-command-line-usage}

**File pacchetto uno:**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` : nome del file da crittografare.
* `dest` : nome del file crittografato risultante.

   Se si specifica una directory, il file crittografato viene salvato automaticamente nella directory specificata con lo stesso nome specificato come file di origine. Tuttavia, non è possibile specificare una directory di destinazione che includa il file di origine.

**Creare pacchetti di più file con la stessa chiave** (per il supporto di velocità bit multiple):

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` : serie di voci di origine delimitate da spazi vuoti per i file che desideri crittografare.
* `dest-directory` : la directory di destinazione in cui desideri scrivere il contenuto crittografato. I file crittografati vengono salvati automaticamente in questa directory utilizzando gli stessi nomi dei file di origine. Tuttavia, la directory di destinazione non può includere alcun file di origine.

**Visualizza informazioni su un file crittografato:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**Visualizza informazioni su un file di metadati:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` è un [!DNL .metadata] che include metadati DRM.

>[!NOTE]
>
>Durante la creazione del pacchetto, Media Packager non può più generare un [!DNL .header] per impostazione predefinita. Per generare un [!DNL .header] file, utilizza `-h` durante l&#39;imballaggio.

**Tabella 3: Opzioni**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, DRM Media Packager cerca <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro corrente. </p> <p>Nota: le opzioni specificate nella riga di comando hanno la precedenza su quelle specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consente di visualizzare informazioni su un file già incluso nel pacchetto. </p> <p class="- topic/p ">I file di origine e di destinazione non sono obbligatori. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadata </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consente di visualizzare informazioni sui metadati esistenti. </p> <p class="- topic/p ">I file di origine e di destinazione non sono obbligatori. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrae i criteri DRM da un file collocato quando si applica questa opzione insieme al <span class="codeph"> d </span> opzione. </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory in cui si trova il file crittografato con un nome di file e un identificatore della policy DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrae l'intestazione DRM da un file collocato quando si applica questa opzione insieme al <span class="codeph"> d </span> opzione. </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory in cui si trova il file crittografato, con il nome e l'estensione del file <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica un identificatore univoco per questo segmento di contenuto. </p> <p class="- topic/p ">Se non si specifica un identificatore, il nome del file di destfile viene applicato automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> chiave </span>= <span class="+ topic/ph pr-d/codeph codeph"> valore </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave/valore personalizzato da aggiungere ai metadati di contenuto. </p> <p class="- topic/p ">È possibile specificare più <span class="codeph"> -k </span> opzioni. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrai metadati da un file in pacchetto quando applichi questa opzione insieme alla <span class="codeph"> d </span> opzione. </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory del file crittografato con un nome di file e un <span class="codeph"> .metadata </span> estensione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. </p> <p class="- topic/p ">Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sovrascrive il file di destinazione senza che venga richiesto se non esiste già. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nomefile [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome del file che include il criterio DRM. </p> <p class="- topic/p ">Se il criterio DRM richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato nel file delle proprietà, è necessario fornire il certificato di trasporto del dominio. </p> <p class="- topic/p ">È possibile specificare più <span class="codeph"> -p </span> opzioni. Per impostazione predefinita, il client applica sempre la prima opzione. I valori specificati nella riga di comando hanno la precedenza su quelli specificati nel file di configurazione. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà di configurazione {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>Per i nomi di proprietà che includono* n*, *n* rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

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
   <td colname="2" class="- topic/entry "> <p>Indica se crittografare i dati script in mp4s. </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> e <i class="+ topic/ph hi-d/i ">onXMP</i> i tag di dati script non vengono mai crittografati anche se si abilita questa opzione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica il livello di crittografia del video. </p> <p class="- topic/p ">Un valore di <span class="codeph"> alta</span> viene utilizzato per crittografare tutto il contenuto video, mentre i valori di <span class="codeph"> media</span> e <span class="codeph"> bassa</span> vengono utilizzati per crittografare parti del contenuto video per i file mp4 che includono contenuto H.264. </p> <p class="- topic/p ">value = <span class="codeph"> alta | medio | bassa</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un valore è maggiore di 0, il numero specificato di secondi di contenuto all'inizio del file non viene crittografato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File del certificato del server licenze utilizzato per crittografare la chiave. </p> <p class="- topic/p ">Il <span class="codeph"> encrypt.keys.asymmetric.certfile</span> specifica un file che include solo il certificato (è possibile utilizzare il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Questa proprietà viene utilizzata ripetutamente per creare un elenco di criteri DRM da applicare al contenuto. <span class="codeph"> n</span> rappresenta un numero intero il cui valore è maggiore o uguale a 1. Per impostazione predefinita, il client utilizza la prima istanza. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server licenze </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certificato di trasporto per il server licenze. </p> <p class="- topic/p ">Questa proprietà specifica un <span class="filepath"> cer</span> file che include solo il certificato (è accettabile il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il file PKCS12 che include le credenziali del packager per la firma del contenuto. </p> <p class="- topic/p ">Il <span class="codeph"> encrypt.sign.certfile</span> deve fare riferimento a un <span class="filepath"> .pfx</span> che include un certificato e una chiave privata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Password che è possibile applicare per proteggere il file specificato da <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Imposta la versione minima del server necessaria per rilasciare le licenze per il contenuto da includere nel pacchetto. </p> <p class="- topic/p ">Specificare x (per Primetime DRM x.0) dove x rappresenta un numero di versione principale. Tutte le versioni dei server precedenti alla versione 3.0 di Adobe Primetime non supportano questa impostazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un criterio DRM <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> richiede la registrazione del dominio con un server che supporti un certificato di trasporto diverso da quello specificato in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, è quindi necessario fornire il certificato di trasporto del dominio necessario. </p> <p class="- topic/p ">Questa proprietà specifica un file che include solo il certificato (è possibile utilizzare il formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave di licenza. </p> <p class="- topic/p ">Se non specifichi una chiave, questa viene generata in modo casuale. Se non si abilita la rotazione delle chiavi, è possibile utilizzare questa chiave per crittografare il contenuto. </p> <p class="- topic/p ">Quando attivate la rotazione dei tasti, potete utilizzare questo tasto per proteggere i tasti di rotazione. La chiave deve avere una lunghezza di 16 byte ed essere specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica se la rotazione delle chiavi è abilitata. </p> <p class="- topic/p ">Se è impostato su false, che è l’impostazione predefinita, la rotazione delle chiavi è disabilitata e il master CEK viene utilizzato per crittografare tutti i campioni nel contenuto. </p> <p class="- topic/p ">Se è impostato su true, la rotazione delle chiavi è abilitata e è possibile utilizzare chiavi diverse per crittografare i segmenti di qualsiasi contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequenza di chiavi ruotate che è possibile specificare per crittografare il contenuto quando è abilitata la rotazione delle chiavi. </p> <p class="- topic/p ">Se non specifichi alcuna chiave, le chiavi vengono generate in modo casuale. Le chiavi devono essere lunghe 16 byte e specificate come valori esadecimali. </p> <p class="- topic/p ">Lo spazio vuoto tra i valori esadecimali è facoltativo. <i class="+ topic/ph hi-d/i ">n</i> deve aumentare in modo monotono, a partire da 1. Quando si specificano più tasti, i tasti vengono spostati nell'ordine indicato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica l'intervallo di tempo, in secondi, durante il quale è possibile applicare una chiave di rotazione per crittografare i campioni di contenuto. </p> <p class="- topic/p ">Trascorso l'intervallo di tempo in cui il contenuto è stato crittografato, viene applicata la chiave di rotazione successiva. Se è stata attivata la rotazione dei tasti ma non è stato specificato alcun intervallo di tempo, i tasti vengono ruotati automaticamente ogni 15 minuti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se questa opzione è impostata su true, non è disponibile un server licenze da cui è possibile ottenere le licenze. </p> <p class="- topic/p ">Le licenze devono essere incorporate o ottenute fuori banda. Il valore predefinito è impostato su false a meno che non si specifichi un valore diverso. Questa opzione è supportata solo in Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
