---
seo-title: Utilizzo della riga di comando
title: Utilizzo della riga di comando
uuid: 5f24f18d-09ef-400a-9404-50a9fcf4316d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Utilizzo della riga di comando {#command-line-usage}

Prima di utilizzare Media Packager, accertatevi di soddisfare i requisiti elencati in Requisiti e che il file di configurazione contenga le informazioni necessarie (consultate il file di configurazione in *Utilizzo delle implementazioni* di riferimento per l&#39;accesso al Adobe .

Media Packager si trova nella [!DNL \Reference Implementation\Command Line tools] directory del DVD. Per cifrare un singolo file, utilizzare la sintassi seguente:

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

* `source` è il file da cifrare.
* `dest` specifica dove verrà scritto il contenuto cifrato. Se viene specificata una directory, il file crittografato verrà salvato in questa cartella utilizzando lo stesso nome file del file di origine, ma la directory non deve essere la directory che contiene il file di origine.

Per cifrare più file con la stessa chiave (per il supporto con bitrate multiplo), utilizzate la sintassi seguente:

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

* `sourcefiles` è una serie di voci sorgente delimitate da spazi bianchi che rappresentano i file da cifrare.
* `dest-directory` specifica dove verrà scritto il contenuto cifrato. I file crittografati verranno salvati in questa cartella utilizzando gli stessi nomi di file dei file sorgente, ma la directory non deve essere la directory che contiene i file sorgente.

Per visualizzare informazioni su un file crittografato, utilizzare la sintassi seguente:

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` è il file crittografato.

Per visualizzare informazioni su un file di metadati, utilizzate la sintassi seguente:

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` è un [!DNL .metadata] file contenente i metadati DRM.

>[!NOTE]
>
>Durante la creazione del pacchetto, per impostazione predefinita Media Packager non genera più un file .header. Per generare questo file, utilizzate l&#39; `-h` opzione durante la creazione del pacchetto.

La tabella seguente contiene le descrizioni delle opzioni della riga di comando mostrate nella sintassi precedente:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il percorso del file di configurazione. Se questa opzione non viene utilizzata, Media Packager cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Mostra informazioni su un file già incluso nel pacchetto. I file di origine e di destinazione non sono richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadata </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Mostra informazioni sui metadati esistenti. I file di origine e di destinazione non sono richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzate questa opzione con <span class="codeph"> -d </span> per estrarre i criteri da un file pacchetto. Un file verrà creato nella stessa directory del file crittografato utilizzando il nome del file e l'identificatore del criterio. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzate with <span class="codeph"> -d </span> per estrarre l'intestazione DRM da un file pacchetto. Un file viene creato nella stessa directory del file crittografato, utilizzando il nome del file e l'estensione <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica un identificatore univoco per questo contenuto. Se non viene specificato alcun identificatore, verrà utilizzato il nome del file di destinazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> value </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave/valore personalizzato da aggiungere ai metadati del contenuto. È possibile specificare più opzioni <span class="codeph"> -k </span> . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzate questa opzione con <span class="codeph"> -d </span> per estrarre i metadati da un file pacchetto. Un file verrà creato nella stessa directory del file crittografato utilizzando il nome del file e l'estensione <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o non </span> è impostato, viene restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sovrascrive il file di destinazione senza richiedere, se esiste già. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nomefile [dominio-trasporto-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome del file contenente il criterio. Se il criterio richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato nel file delle proprietà, deve essere fornito anche il certificato di trasporto del dominio. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -p </span> e per impostazione predefinita il primo verrà utilizzato dal client. I valori specificati nella riga di comando hanno precedenza rispetto a quelli specificati nel file di configurazione. </p> </td> 
  </tr> 
 </tbody> 
</table>

