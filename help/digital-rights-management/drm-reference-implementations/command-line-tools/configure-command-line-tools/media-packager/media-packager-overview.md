---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# DRM Media Packager {#media-packager}

Utilizza Media Packager ( [!DNL AdobePackager.jar]) per specificare un criterio DRM da applicare al contenuto e per specificare quale parte del contenuto cifrare. Ad esempio, puoi specificare che il gestore di pacchetti deve crittografare i dati video, ma non i dati audio.

Prima di eseguire [!DNL AdobePackager.jar], è necessario impostare le proprietà nella sezione Proprietà di Media Packager del file di configurazione.

>[!NOTE]
>
>È inoltre possibile specificare tutte le proprietà di Media Packager dalla riga di comando.

## Utilizzo della riga di comando di Media Packager {#media-packager-command-line-usage}

**Crea un pacchetto di un file:**

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

* `source` - Il nome del file da crittografare.
* `dest` - Il nome del file crittografato risultante.

   Se si specifica una directory, il file crittografato viene salvato automaticamente nella directory specificata con lo stesso nome di file specificato come file di origine. Tuttavia, non è possibile specificare una directory di destinazione che includa il file di origine.

**Creare pacchetti di più file con la stessa chiave**  (per il supporto a più bit rate):

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

* `sourcefiles` - Serie di voci di origine delimitate da spazi bianchi per i file da crittografare.
* `dest-directory` - La directory di destinazione in cui si desidera scrivere il contenuto crittografato. I file crittografati vengono salvati automaticamente in questa directory utilizzando gli stessi nomi dei file di origine. Tuttavia, la directory di destinazione non può includere file di origine.

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

* `metadatafile` è un  [!DNL .metadata] file che include metadati DRM.

>[!NOTE]
>
>Durante la creazione del pacchetto, Media Packager non può più generare un file [!DNL .header] per impostazione predefinita. Per generare un file [!DNL .header], utilizza l&#39;opzione `-h` durante la creazione del pacchetto.

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configurare il file </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e il percorso del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, il DRM Media Packager cerca <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro corrente. </p> <p>Nota:  Le opzioni specificate nella riga di comando hanno la precedenza sulle opzioni specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consente di visualizzare informazioni su un file già compilato. </p> <p class="- topic/p ">I file di origine e di destinazione non sono necessari. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consente di visualizzare informazioni sui metadati esistenti. </p> <p class="- topic/p ">I file di origine e di destinazione non sono necessari. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrae i criteri DRM da un file compilato quando applichi questa opzione insieme all'opzione <span class="codeph"> -d </span>. </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory in cui si trova il file crittografato con un nome di file e un identificatore di criteri DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrae l'intestazione DRM da un file compilato quando applichi questa opzione insieme all'opzione <span class="codeph"> -d </span>. </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory in cui si trova il file crittografato, con il nome del file e l'estensione <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica un identificatore univoco per il segmento di contenuto. </p> <p class="- topic/p ">Se non si specifica un identificatore, il nome del file di destinazione viene applicato automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> chiave </span>= <span class="+ topic/ph pr-d/codeph codeph"> valore </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave/valore personalizzata da aggiungere ai metadati del contenuto. </p> <p class="- topic/p ">Puoi specificare più opzioni <span class="codeph"> -k </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrai i metadati da un file compilato quando applichi questa opzione insieme all'opzione <span class="codeph"> -d </span>. </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory del file crittografato con un nome di file e un'estensione <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. </p> <p class="- topic/p ">Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sovrascrive il file di destinazione senza che venga richiesto, a meno che non esista già. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nomefile [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome del file che include il criterio DRM. </p> <p class="- topic/p ">Se il criterio DRM richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato nel file delle proprietà, devi fornire il certificato di trasporto del dominio. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -p </span>. Per impostazione predefinita, il client applica sempre la prima opzione. I valori specificati nella riga di comando hanno la precedenza su quelli specificati nel file di configurazione. </p> </td> 
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
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare il contenuto video. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare l'audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Indica se crittografare i dati di script in mp4s. </p> <p><i class="+ topic/ph hi-d/i ">I tag dati </i> onMetaDatae  <i class="+ topic/ph hi-d/i "></i> onXMPscript non vengono mai crittografati anche se abiliti questa opzione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica il livello di crittografia video. </p> <p class="- topic/p ">Un valore di <span class="codeph"> high</span> viene utilizzato per cifrare tutti i contenuti video, mentre i valori di <span class="codeph"> medium</span> e <span class="codeph"> low</span> vengono utilizzati per cifrare parti del contenuto video per file mp4 che includono contenuto H.264. </p> <p class="- topic/p ">value = <span class="codeph"> high | media | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsNon crittografato</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un valore è maggiore di 0, il numero specificato di secondi di contenuto all'inizio del file non viene crittografato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">File del certificato del server di licenza utilizzato per crittografare la chiave. </p> <p class="- topic/p ">La proprietà <span class="codeph"> encrypt.keys.asymmetric.certfile</span> specifica un file che include solo il certificato (il formato PEM o DER è accettabile). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Questa proprietà viene utilizzata ripetutamente per creare un elenco di criteri DRM da applicare al contenuto. <span class="codeph"> </span> rappresenta un numero intero il cui valore è maggiore o uguale a 1. Per impostazione predefinita, il client utilizza la prima istanza. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server licenze </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certificato di trasporto per il server licenze. </p> <p class="- topic/p ">Questa proprietà specifica un file <span class="filepath"> .cer</span> che include solo il certificato (il formato PEM o DER è accettabile). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il file PKCS12 che include le credenziali del packager per la firma del contenuto. </p> <p class="- topic/p ">Il file <span class="codeph"> encrypt.sign.certfile</span> deve fare riferimento a un file <span class="filepath"> .pfx</span> che include un certificato e una chiave privata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Password che puoi applicare per proteggere il file specificato da <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Imposta la versione minima del server necessaria per il rilascio delle licenze per il contenuto in fase di creazione del pacchetto. </p> <p class="- topic/p ">Specifica x (per Primetime DRM x.0) dove x rappresenta un numero di rilascio principale. Tutte le versioni dei server che precedono Adobe Primetime versione 3.0 non supportano questa impostazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un criterio DRM <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> richiede la registrazione del dominio con un server che supporta un certificato di trasporto diverso da quello specificato in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, è necessario fornire il certificato di trasporto del dominio necessario. </p> <p class="- topic/p ">Questa proprietà specifica un file che include solo il certificato (il formato PEM o DER è accettabile). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave di licenza. </p> <p class="- topic/p ">Se non specifichi una chiave, la chiave viene generata in modo casuale. Se non abiliti la rotazione delle chiavi, puoi utilizzare questa chiave per crittografare il contenuto. </p> <p class="- topic/p ">Quando si abilita la rotazione dei tasti, è possibile utilizzare questo tasto per proteggere i tasti di rotazione. La chiave deve avere una lunghezza di 16 byte ed essere specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rot.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica se la rotazione delle chiavi è abilitata. </p> <p class="- topic/p ">Se è impostato su false, che è l’impostazione predefinita, la rotazione della chiave viene disabilitata e la CEK master viene utilizzata per crittografare tutti i campioni nel contenuto. </p> <p class="- topic/p ">Se è impostato su true, la rotazione delle chiavi è abilitata e puoi utilizzare chiavi diverse per crittografare i segmenti di qualsiasi contenuto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rot.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequenza di chiavi ruotate che è possibile specificare per crittografare il contenuto quando la rotazione delle chiavi è abilitata. </p> <p class="- topic/p ">Se non specifichi alcuna chiave, le chiavi vengono generate in modo casuale. Le chiavi devono avere una lunghezza di 16 byte e devono essere specificate come valori esadecimali. </p> <p class="- topic/p ">Lo spazio vuoto tra i valori esadecimali è facoltativo. <i class="+ topic/ph hi-d/i "></i> deve aumentare monotonicamente, a partire da 1. Quando specifichi più chiavi, le chiavi vengono sottoposte a ciclo continuo nell’ordine indicato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotv.Interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica l’intervallo di tempo in secondi durante il quale è possibile applicare una chiave di rotazione per crittografare gli esempi di contenuto. </p> <p class="- topic/p ">Dopo che è trascorso l’intervallo di tempo in cui il contenuto è stato crittografato, viene quindi applicata la chiave di rotazione successiva. Se hai attivato la rotazione dei tasti ma non hai specificato alcun intervallo di tempo, i tasti vengono ruotati automaticamente ogni 15 minuti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se questa opzione è impostata su true, non è disponibile un server licenze da cui è possibile ottenere le licenze. </p> <p class="- topic/p ">Le licenze devono essere incorporate o ottenute fuori banda. Il valore predefinito è impostato su false a meno che non si specifichi un valore diverso. Questa opzione è supportata solo in Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>