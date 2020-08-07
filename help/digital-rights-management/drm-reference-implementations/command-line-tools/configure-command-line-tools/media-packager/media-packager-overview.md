---
description: 'null'
seo-description: 'null'
seo-title: Panoramica
title: Panoramica
uuid: f4474837-9460-479d-89c2-dd697e0fb997
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 0%

---


# DRM Media Packager {#media-packager}

Utilizzate Media Packager ( [!DNL AdobePackager.jar]) per specificare un criterio DRM da applicare al contenuto e per specificare quale parte del contenuto cifrare. Ad esempio, potete specificare che il packager deve cifrare i dati video, ma non i dati audio.

Prima di eseguire [!DNL AdobePackager.jar], è necessario impostare le proprietà nella sezione Proprietà di Media Packager del file di configurazione.

>[!NOTE]
>
>Potete inoltre specificare tutte le proprietà di Media Packager dalla riga di comando.

## Utilizzo della riga di comando di Media Packager {#media-packager-command-line-usage}

**Pacchetto di un file:**

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

* `source` - Il nome del file da cifrare.
* `dest` - Il nome del file crittografato risultante.

   Se si specifica una directory, il file crittografato viene salvato automaticamente nella directory specificata con lo stesso nome di file specificato come file di origine. Tuttavia, non potete specificare una directory di destinazione che includa il file di origine.

**Create pacchetti di più file con la stessa chiave** (per il supporto con bitrate multiplo):

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

* `sourcefiles` - Serie di voci sorgente delimitate da spazi bianchi per i file da cifrare.
* `dest-directory` - La directory di destinazione in cui si desidera scrivere il contenuto crittografato. I file crittografati vengono salvati automaticamente in questa directory utilizzando gli stessi nomi di file dei file sorgente. Tuttavia, la directory di destinazione non può includere alcun file sorgente.

**Visualizzare informazioni su un file crittografato:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**Visualizzare informazioni su un file di metadati:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` è un [!DNL .metadata] file che include i metadati DRM.

>[!NOTE]
>
>Durante la creazione del pacchetto, Media Packager non è più in grado di generare un [!DNL .header] file per impostazione predefinita. Per generare un [!DNL .header] file, utilizzate l&#39; `-h` opzione durante la creazione del pacchetto.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p> <p class="- topic/p ">Se non specificate un nome o una posizione, DRM Media Packager ricerca <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro corrente. </p> <p>Nota:  Le opzioni specificate nella riga di comando hanno la precedenza rispetto alle opzioni specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consente di visualizzare informazioni su un file già incluso nel pacchetto. </p> <p class="- topic/p ">I file di origine e di destinazione non sono richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadata </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consente di visualizzare informazioni sui metadati esistenti. </p> <p class="- topic/p ">I file di origine e di destinazione non sono richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrae i criteri DRM da un file pacchetto quando si applica questa opzione insieme all'opzione <span class="codeph"> -d </span> . </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory in cui si trova il file crittografato con un nome file e un identificatore di criteri DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estrae l'intestazione DRM da un file incluso nel pacchetto quando si applica questa opzione insieme all'opzione <span class="codeph"> -d </span> . </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory in cui si trova il file crittografato, con il nome del file e l'estensione <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica un identificatore univoco per questo segmento di contenuto. </p> <p class="- topic/p ">Se non si specifica un identificatore, il nome del file di destinazione viene applicato automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> value </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave/valore personalizzato da aggiungere ai metadati del contenuto. </p> <p class="- topic/p ">Potete specificare più opzioni <span class="codeph"> -k </span> . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estraete i metadati da un file compresso quando applicate questa opzione insieme all'opzione <span class="codeph"> -d </span> . </p> <p class="- topic/p ">Un file viene creato automaticamente nella stessa directory del file crittografato con un nome file e un'estensione <span class="codeph"> .metadata </span> . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. </p> <p class="- topic/p ">Se il file di destinazione esiste già e <span class="codeph"> -o non </span> è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sovrascrive il file di destinazione senza che venga richiesto di specificarlo, a meno che non esista già. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nomefile [dominio-trasporto-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome del file che include il criterio DRM. </p> <p class="- topic/p ">Se il criterio DRM richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato nel file delle proprietà, è necessario fornire il certificato di trasporto del dominio. </p> <p class="- topic/p ">Potete specificare più opzioni <span class="codeph"> -p </span> . Per impostazione predefinita, il client applica sempre la prima opzione. I valori specificati nella riga di comando hanno la precedenza su quelli specificati nel file di configurazione. </p> </td> 
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
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se crittografare l'audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Indica se crittografare i dati di script in mp4s. </p> <p><i class="+ topic/ph hi-d/i ">i tag di dati di script onMetaData</i> e <i class="+ topic/ph hi-d/i ">onXMP</i> non vengono mai crittografati persino se si abilita questa opzione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica il livello di cifratura del video. </p> <p class="- topic/p ">Per cifrare tutto il contenuto video viene utilizzato un valore <span class="codeph"> elevato</span> , mentre per cifrare parti del contenuto video per i file mp4 che includono contenuto H.264 vengono utilizzati valori <span class="codeph"> medi</span> e <span class="codeph"> bassi</span> . </p> <p class="- topic/p ">value = <span class="codeph"> high | medium | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.SecondiNon crittografato</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un valore è maggiore di 0, il numero specificato di secondi di contenuto all'inizio del file non viene crittografato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il file del certificato del server licenze utilizzato per crittografare la chiave. </p> <p class="- topic/p ">La proprietà <span class="codeph"> encrypt.keys.asymmetric.certfile</span> specifica un file che include solo il certificato (il formato PEM o DER è accettabile). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Questa proprietà viene utilizzata ripetutamente per creare un elenco di criteri DRM da applicare al contenuto. <span class="codeph"> n</span> rappresenta un numero intero il cui valore è uguale o superiore a 1. Per impostazione predefinita, il client utilizza la prima istanza. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">L’URL del server licenze </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il certificato di trasporto per il server licenze. </p> <p class="- topic/p ">Questa proprietà specifica un file <span class="filepath"> .cer</span> che include solo il certificato (è accettabile sia il formato PEM che DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il file PKCS12 che include le credenziali del packager per la firma del contenuto. </p> <p class="- topic/p ">Il file <span class="codeph"> encrypt.sign.certfile</span> deve fare riferimento a un file <span class="filepath"> .pfx</span> che include un certificato e una chiave privata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La password che è possibile applicare per proteggere il file specificato da <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Imposta la versione server minima necessaria per rilasciare licenze per il contenuto in fase di creazione del pacchetto. </p> <p class="- topic/p ">Specificate x (per Primetime DRM x.0) dove x rappresenta un numero di rilascio principale. Tutte le versioni dei server che precedono  versione 3.0 di Adobe Primetime non supportano questa impostazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se un criterio DRM <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> richiede la registrazione del dominio con un server che supporta un certificato di trasporto diverso da quello specificato in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, è necessario fornire il certificato di trasporto del dominio richiesto. </p> <p class="- topic/p ">Questa proprietà specifica un file che include solo il certificato (il formato PEM o DER è accettabile). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave di licenza. </p> <p class="- topic/p ">Se non si specifica una chiave, la chiave viene generata in modo casuale. Se non si abilita la rotazione delle chiavi, è possibile utilizzare questa chiave per cifrare il contenuto. </p> <p class="- topic/p ">Quando si abilita la rotazione delle chiavi, è possibile utilizzare questo tasto per proteggere i tasti di rotazione. La chiave deve avere una lunghezza di 16 byte ed essere specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica se la rotazione della chiave è abilitata. </p> <p class="- topic/p ">Se è impostata su false, che è l'impostazione predefinita, la rotazione delle chiavi è disabilitata e il CEK master viene utilizzato per crittografare tutti i campioni nel contenuto. </p> <p class="- topic/p ">Se è impostata su true, la rotazione delle chiavi è abilitata e per cifrare segmenti di qualsiasi contenuto è possibile utilizzare chiavi diverse. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequenza di chiavi ruotate che è possibile specificare per cifrare il contenuto quando è abilitata la rotazione delle chiavi. </p> <p class="- topic/p ">Se non si specificano chiavi, le chiavi vengono generate in modo casuale. Le chiavi devono avere una lunghezza di 16 byte e devono essere specificate come valori esadecimali. </p> <p class="- topic/p ">Lo spazio vuoto tra i valori esadecimali è facoltativo. <i class="+ topic/ph hi-d/i ">A partire da 1,</i> deve essere in aumento monotonico. Quando si specificano più chiavi, i tasti passano in sequenza nell'ordine indicato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica l'intervallo di tempo in secondi durante il quale è possibile applicare una chiave di rotazione per cifrare gli esempi di contenuto. </p> <p class="- topic/p ">Una volta trascorso l'intervallo di tempo in cui il contenuto è stato crittografato, viene applicata la chiave di rotazione successiva. Se hai attivato la rotazione delle chiavi ma non hai specificato alcun intervallo di tempo, i tasti vengono ruotati automaticamente ogni 15 minuti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se questa opzione è impostata su true, il server licenze da cui è possibile ottenere le licenze non è disponibile. </p> <p class="- topic/p ">Le licenze devono essere incorporate o ottenute fuori banda. Il valore predefinito è false, a meno che non venga specificato un valore diverso. Questa opzione è supportata solo in Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>