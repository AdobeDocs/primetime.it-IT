---
description: L'interfaccia Video Encoder di AVE restituisce queste notifiche di riproduzione video nell'oggetto metadati NATIVE_ERROR.
title: Valori di riproduzione video NATIVE_ERROR
exl-id: a4476bbe-a62b-40cf-9795-cd209683c572
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 6%

---

# NATIVE_ERROR: valori di riproduzione video{#native-error-video-playback-values}

L&#39;interfaccia Video Encoder di AVE restituisce queste notifiche di riproduzione video nell&#39;oggetto metadati NATIVE_ERROR.

<table> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Valore per la chiave di metadati NATIVE_ERROR_CODE </th> 
   <th colname="col2" class="entry"> Valore per la chiave di metadati NATIVE_ERROR_NAME </th> 
   <th colname="col3" class="entry"> Descrizione </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> FINE_PERIODO</span> </td> 
   <td colname="col3"> Fine del periodo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> OPERAZIONE RIUSCITA</span> </td> 
   <td colname="col3"> Operazione completata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operazione asincrona. La richiesta di operazione è stata effettuata. Le informazioni di successo/errore saranno disponibili in seguito. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Operazione non possibile a causa della condizione di fine file (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> Errore del decodificatore in fase di esecuzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Impossibile aprire il decodificatore hardware. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND </span> </td> 
   <td colname="col3"> Impossibile individuare la risorsa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> Errore generico. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR </span> </td> 
   <td colname="col3"> Condizione di errore da cui il motore video non può essere ripristinato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERY </span> </td> 
   <td colname="col3"> Errore di rete, tentativo di ripristino in corso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> Impossibile determinare la dimensione della risorsa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTATO </span> </td> 
   <td colname="col3"> Funzionalità non implementata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> MEMORIA_ESAURITA </span> </td> 
   <td colname="col3"> Memoria insufficiente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> Errore durante l'analisi del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN </span> </td> 
   <td colname="col3"> La risorsa ha una dimensione, ma è sconosciuta. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> Condizione di underflow. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> Configurazione non supportata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION </span> </td> 
   <td colname="col3"> Operazione non supportata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> Non ancora inizializzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> Parametro non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operazione non consentita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> Operazione consentita solo se in pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> Impossibile utilizzare l'operazione su file solo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> L’operazione di ricerca precedente è ancora in corso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> Risorsa non specificata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> Il valore specificato non è compreso nell'intervallo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Tempo di ricerca non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> Il file specificato non è conforme alla sintassi prevista. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> Impossibile creare un componente essenziale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Impossibile creare il contesto DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> Tipo di contenitore non supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Ricerca non riuscita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Codec non supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> RETE_NON DISPONIBILE</span> </td> 
   <td colname="col3"> Rete non disponibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> ERRORE_DI_RETE</span> </td> 
   <td colname="col3"> Errore nell’ottenere dati dalla rete. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> OVERFLOW</span> </td> 
   <td colname="col3"> Overflow. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Profilo video non supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> Tentativo di operazione su un periodo di blocco o su un periodo non ancora caricato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> La durata di sostituzione specificata non è valida o si estende oltre la fine del flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CHIAMATO_DA_SBAGLIATO_THREAD</span> </td> 
   <td colname="col3"> Impossibile chiamare l'API dal thread errato. Principalmente, per gli elementi API che devono essere chiamati solo dal thread principale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Errore di lettura del frammento. Nessun failover presente. Il motore proverà a leggere il frammento successivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> INTERROTTO</span> </td> 
   <td colname="col3"> Operazione interrotta da una chiamata di interruzione o eliminazione esplicita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Impossibile riprodurre questa versione del supporto HLS. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Impossibile eseguire il failover. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> Timeout del download HTTP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> La connessione di rete dell'utente non è attiva. La riproduzione potrebbe interrompersi in qualsiasi momento e riprenderà quando la connessione sarà disponibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Nessun profilo di velocità in bit utilizzabile trovato nel flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> Il manifesto ha una firma non valida. Il test della firma del manifesto non è riuscito. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> IMPOSSIBILE_CARICARE_PLAYLIST</span> </td> 
   <td colname="col3"> Impossibile caricare una playlist. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> Impossibile eseguire la sostituzione specificata in un'API di inserimento. Ciò significa che l'inserimento è riuscito, ma la sostituzione non è riuscita. La sostituzione potrebbe non riuscire se il manifesto da sostituire è stato rimosso dalla timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_AYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM sta passando a un profilo asimmetrico. È previsto che tutti i profili siano allineati in durata. In caso contrario, verrà visualizzato questo avviso e potrebbero verificarsi salti nella riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVE_BACKWARD</span> </td> 
   <td colname="col3"> La finestra Live deve essere spostata solo in avanti. In caso contrario, questo avviso verrà generato e la finestra non verrà letta. Per questo motivo, potrebbero verificarsi salti (o pause lunghe/di arresto) nella riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> La finestra Live è stata spostata oltre il periodo corrente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> La lunghezza del contenuto segnalata dal server HTTP non corrisponde alla dimensione effettiva del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> Il lettore multimediale non è in grado di leggere ulteriormente perché ha raggiunto l’ora impostata dall’API setHoldAt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3"> Il lettore multimediale non è in grado di caricare i segmenti perché ha raggiunto la fine della finestra live. Il caricamento del segmento riprenderà quando il server aggiunge nuovi file multimediali alla finestra live. Questo stato viene generalmente raggiunto se: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">BufferTime troppo alto (uguale o superiore alla durata della finestra attiva). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Una combinazione di una o più API di inserimento/cancellazione ha sostituito più supporti di quelli aggiunti. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">Il periodo successivo è un periodo live con una sostituzione dei contenuti multimediali in sospeso (a causa della chiamata API InsertBy) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> L'interfoliazione audio e video nel supporto non viene eseguita correttamente. Si tratta di un errore di packaging. L’avviso viene inviato quando la differenza supera i due secondi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> La riproduzione HLS non è stata abilitata nel Flash Player. Consulta AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> Il decodificatore ha ricevuto un campione non valido che non può essere decodificato. In genere non si tratta di un errore irreversibile, ma indica che potrebbero verificarsi errori nell’audio/video. Troppe istanze di questo errore indicano una codifica non valida o un file non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Dopo l'avvio della riproduzione, l'intervallo Inserisci/Sostituisci non deve contenere l'intestazione di lettura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> Gli inserimenti post-roll non sono consentiti nei file multimediali live. Sono tuttavia consentiti dopo che il server ha contrassegnato il supporto come completo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Un problema molto raro che non dovrebbe mai accadere. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> Il flusso non segue la raccomandazione di imballaggio di inserire sempre H264 SPS/PPS in un AVCC. Potrebbero essere visualizzati problemi di ricerca/riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARZIALE_SOSTITUZIONE</span> </td> 
   <td colname="col3"> La sostituzione specificata in un’API di inserimento è stata eseguita solo parzialmente. Ciò si verifica quando replaceDuration si estende sulla durata della sequenza temporale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RAPPRESENTAZIONE_M3U8_ERROR</span> </td> 
   <td colname="col3"> Errore durante il caricamento della playlist della rappresentazione. Questo è solo per AVE, non per FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> L'operazione non esegue alcuna operazione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> Il segmento non può essere riprodotto e viene saltato in caso di errore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Modalità di rendering non compatibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> Il protocollo Web utilizzato nell'URL non è supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Errore durante l'analisi del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> Il file manifesto è stato modificato in modo imprevisto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Impossibile eseguire un'operazione di divisione su una sequenza temporale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Impossibile eseguire un'operazione di cancellazione su una sequenza temporale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Impossibile ottenere il frammento successivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Nessuna timeline presente in una struttura di dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> Nessun listener trovato in una struttura dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Impossibile avviare l'audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> Nessun sink audio presente in una struttura di dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Impossibile aprire il file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Impossibile scrivere su un file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Impossibile leggere da un file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Errore nell’analisi dei dati ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> Caricamento del contenuto non riuscito a causa di restrizioni di protezione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> La durata della sequenza temporale è troppo breve. Se si tratta di un flusso live, può verificarsi un buffering frequente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> Lo streaming è stato convertito in streaming solo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> Lo streaming è stato cambiato da "solo audio" a "video". </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> CHIAVE_NON_TROVATA </span> </td> 
   <td colname="col3"> Impossibile trovare la chiave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> Chiave non valida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> Il server chiavi non restituisce alcuna chiave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Impossibile gestire l'aggiornamento del manifesto principale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTS_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> È stata rilevata una discontinuità nell’ora non segnalata (PTS). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> È stata rilevata una discontinuità audio e video senza corrispondenza. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Si è verificato un errore durante la riproduzione del contenuto multimediale in <i>riproduzione con trucco</i> modalità. La modalità di riproduzione dei brani viene terminata e il flusso viene messo in pausa. Chiamata <span class="codeph"> Play()</span> per riprodurre il supporto in modalità normale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVE_AHEAD</span> </td> 
   <td colname="col3"> Il giocatore è fuori dalla finestra dal vivo e deve cercare in avanti per recuperare. </td> 
  </tr> 
 </tbody> 
</table>
