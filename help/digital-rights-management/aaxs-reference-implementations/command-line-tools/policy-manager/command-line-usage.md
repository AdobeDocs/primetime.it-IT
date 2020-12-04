---
seo-title: Utilizzo della riga di comando
title: Utilizzo della riga di comando
uuid: e549a98e-b027-4472-8860-6aa1d56d4a8b
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---


# Utilizzo della riga di comando {#command-line-usage}

Prima di utilizzare Policy Manager, accertati di soddisfare i requisiti elencati in Requisiti.

Policy Manager si trova nella directory [!DNL \Reference Implementation\Command Line Tools] del DVD. Per eseguire lo strumento, utilizzare la sintassi seguente:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

La tabella seguente contiene le descrizioni delle azioni della riga di comando mostrate nella sintassi precedente:

| Azione riga di comando | Descrizione |
|---|---|
| `new` | Crea un nuovo criterio. |
| `detail` | Descrive un criterio esistente. |
| `update` | Aggiorna un criterio esistente. |

La tabella seguente descrive le opzioni della riga di comando che è possibile specificare insieme alla sintassi precedente:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il percorso del file di configurazione. Se questa opzione non viene utilizzata, Policy Manager cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. Le opzioni specificate nella riga di comando hanno la precedenza su quelle presenti nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascrivetelo senza richiedere l'invio di richieste. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, verrà restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che il criterio dispone di una licenza radice. Non sono consentiti aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data prima della quale le licenze saranno valide. Specificare come <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1 dicembre 2008. Il valore deve essere maggiore del valore di <span class="codeph"> -s </span>, se presente. Questa opzione non può essere utilizzata con <span class="codeph"> -r </span>. Per rimuovere la data di fine durante l'aggiornamento di un criterio, utilizzare <span class="codeph"> -e </span> senza specificare una data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La durata (minuti) della protezione del contenuto tramite questo criterio è valida, a partire da quando il contenuto è protetto con il packager. Il valore deve essere non negativo. Questa opzione non può essere utilizzata con <span class="codeph"> -e </span>. Per rimuovere la durata dell'aggiornamento di un criterio, utilizzate <span class="codeph"> -r </span> senza specificare un numero di minuti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data di validità delle licenze. Specificare come <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1 dicembre 2008. Il valore deve essere minore del valore di <span class="codeph"> -e </span>, se presente. Questa opzione non può essere utilizzata con <span class="codeph"> -r </span>. Per rimuovere la data di inizio durante l'aggiornamento di un criterio, utilizzare <span class="codeph"> -s </span> senza specificare una data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La finestra di riproduzione (il numero di minuti in cui il contenuto può essere visualizzato, a partire dalla prima riproduzione). Se questa opzione non è specificata o se si utilizza <span class="codeph"> -w </span> senza specificare il numero di minuti, non vi è alcun limite per la finestra di riproduzione. Il valore deve essere non negativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Durata del caching delle licenze in minuti, ovvero l'ora in cui una licenza può essere memorizzata nella cache del punto vendita licenze del cliente dopo che il server ha rilasciato la licenza. Il valore deve essere non negativo. Specificare <span class="codeph"> -l 0 </span> per indicare che il caching delle licenze non è consentito. Utilizzare <span class="codeph"> -l </span> senza specificare un numero di minuti per il caching delle licenze illimitato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -data di scadenza  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data di fine del caching delle licenze (la data dopo la quale le licenze non possono essere memorizzate nella cache nell'archivio licenze del cliente, dopo che il server ha rilasciato la licenza). Specificare come <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>o<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1 dicembre 2008. Utilizzare <span class="codeph"> -l </span> senza specificare un numero di minuti per il caching delle licenze illimitato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lo spazio dei nomi di autenticazione. Se specificato, il client deve autenticarsi con un nome utente e una password emessi dall'autorità specificata. Questa opzione non può essere utilizzata con <span class="codeph"> -x </span>. Non sono consentiti aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consenti accesso anonimo. Questa opzione non può essere utilizzata con <span class="codeph"> -authNS </span>. Non sono consentiti aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[:  <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti  di applicazioni AIR consentite per riprodurre contenuto protetto. Utilizzate questa opzione per limitare quali editori, applicazioni e versioni possono accedere al contenuto protetto tramite questo criterio. </p> <p class="- topic/p ">Se <i class="+ topic/ph hi-d/i ">appId</i> non è specificato, sono consentite tutte le applicazioni per l'editore <i class="+ topic/ph hi-d/i ">pubId</i>. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">I numeri </i> di  <i class="+ topic/ph hi-d/i "></i> versione minima e massima sono facoltativi. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -air </span> per consentire più applicazioni. Se non vengono specificate applicazioni AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, utilizzate -air senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist nome  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valore  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client DRM non potevano accedere al contenuto protetto. Il valore è costituito da coppie nome:valore separate da virgola con il seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante un aggiornamento, utilizzare <span class="codeph"> -drmBlacklist </span> senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i client DRM devono avere il livello di protezione minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalogico NO_PROTECTION | USE_IF_AVAILABLE | RICHIESTO | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Limiti di protezione dell'uscita analogica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | RICHIESTO | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli per la protezione dell'output digitale. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist  </span> <i class="+ topic/ph hi-d/i ">coppie nome/</i> <span class="+ topic/ph pr-d/codeph codeph">   </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> valore  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I tempi di esecuzione dell'applicazione non consentivano l'accesso al contenuto protetto. Il valore è costituito da coppie nome:valore separate da virgola con il seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | domanda | release= stringValue  </span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante un aggiornamento, utilizzare <span class="codeph"> -runtimeBlacklist </span> senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i runtime dell'applicazione devono avere il livello di protezione minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= file_swf  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti  di applicazioni SWF consentite per riprodurre contenuto protetto. È possibile specificare più opzioni swf per consentire l'utilizzo di più applicazioni. Se non vengono specificate applicazioni AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, utilizzate -swf senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. Per identificare un file SWF in base al relativo valore hash, specificate il file SWF per il quale calcolare l'hash e il tempo massimo per consentire il completamento della verifica SWF (in secondi). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la/i chiave/i personalizzata/i da aggiungere al criterio. È possibile specificare più opzioni <span class="codeph"> -k </span>. Durante l'aggiornamento, utilizzare <span class="codeph"> -k </span> senza gli argomenti rimanenti per rimuovere tutte le proprietà. L'interpretazione o la gestione di questi dati è completamente all'altezza dell'implementazione del server licenze di accesso al Adobe . </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge una proprietà personalizzata che verrà visualizzata nella licenza generata per ciascun client. È possibile specificare più opzioni <span class="codeph"> -p </span> per aggiungere più proprietà. Durante un aggiornamento, utilizzare <span class="codeph"> -p </span> senza gli argomenti rimanenti per rimuovere tutte le proprietà. L'interpretazione o la gestione di questi dati è completamente all'implementazione dell'applicazione client. </p> </td> 
  </tr> 
 </tbody> 
</table>

