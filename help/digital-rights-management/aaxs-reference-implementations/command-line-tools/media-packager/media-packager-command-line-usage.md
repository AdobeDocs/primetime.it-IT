---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Utilizzo della riga di comando {#command-line-usage}

Prima di utilizzare Media Packager, accertati di soddisfare i requisiti elencati in Requisiti e che il file di configurazione contenga le informazioni richieste (vedi File di configurazione nella sezione *Utilizzo delle implementazioni di riferimento di accesso Adobe*.

Media Packager è in [!DNL \Reference Implementation\Command Line tools] sul DVD. Per crittografare un singolo file, utilizzare la sintassi seguente:

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

* `source` file da crittografare.
* `dest` specifica dove verrà scritto il contenuto crittografato. Se si specifica una directory, il file crittografato verrà salvato in questa cartella con lo stesso nome del file di origine, ma la directory non deve essere quella che contiene il file di origine.

Per crittografare più file con la stessa chiave (per il supporto della velocità bit multipla), utilizzare la sintassi seguente:

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

* `sourcefiles` è una serie di voci di origine delimitate da spazi vuoti che rappresentano i file da crittografare.
* `dest-directory` specifica dove verrà scritto il contenuto crittografato. I file crittografati verranno salvati in questa cartella utilizzando gli stessi nomi dei file di origine, ma la directory non deve essere la directory che contiene i file di origine.

Per visualizzare informazioni su un file crittografato, utilizzare la sintassi seguente:

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` è il file crittografato.

Per visualizzare le informazioni su un file di metadati, utilizzare la sintassi seguente:

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` è un [!DNL .metadata] file contenente i metadati DRM.

>[!NOTE]
>
>Durante la creazione del pacchetto, Media Packager non genererà più un file .header per impostazione predefinita. Per generare questo file, utilizza `-h` durante l&#39;imballaggio.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la posizione del file di configurazione. Se questa opzione non viene utilizzata, Media Packager cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Mostra informazioni su un file già incluso nel pacchetto. I file di origine e di destinazione non sono obbligatori. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadata </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Mostra informazioni sui metadati esistenti. I file di origine e di destinazione non sono obbligatori. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizza questa opzione con <span class="codeph"> d </span> per estrarre le policy da un file in pacchetto. Un file verrà creato nella stessa directory del file crittografato utilizzando il nome del file e l’identificatore della policy. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Uso con <span class="codeph"> d </span> per estrarre l'intestazione DRM da un file collocato. Un file viene creato nella stessa directory del file crittografato, utilizzando il nome e l’estensione del file <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica un identificatore univoco per questo contenuto. Se non viene specificato alcun identificatore, verrà utilizzato il nome del file di destinazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> chiave </span>= <span class="+ topic/ph pr-d/codeph codeph"> valore </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica una chiave/valore personalizzato da aggiungere ai metadati di contenuto. Più <span class="codeph"> -k </span> è possibile specificare le opzioni. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizza questa opzione con <span class="codeph"> d </span> per estrarre metadati da un file in pacchetto. Verrà creato un file nella stessa directory del file crittografato utilizzando il nome e l'estensione del file <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, verrà restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sovrascrive il file di destinazione senza chiedere conferma, se esiste già. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nomefile [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome del file contenente la policy. Se il criterio richiede la registrazione del dominio con un server che utilizza un certificato di trasporto diverso da quello specificato nel file delle proprietà, è necessario fornire anche il certificato di trasporto del dominio. </p> <p class="- topic/p ">Più <span class="codeph"> -p </span> è possibile specificare le opzioni e il client utilizzerà il primo per impostazione predefinita. I valori specificati nella riga di comando hanno la precedenza su quelli specificati nel file di configurazione. </p> </td> 
  </tr> 
 </tbody> 
</table>
