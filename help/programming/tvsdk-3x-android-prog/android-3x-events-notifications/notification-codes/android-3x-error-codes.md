---
title: Codici di errore PSDK
description: Informazioni su vari codici di errore, avvisi e codici di errore nativi.
translation-type: tm+mt
source-git-commit: eddc327087411a6214cfd8dafef66b850a603f97

---


# Codici di errore PSDK {#psdk-error-codes}

Continua a leggere per conoscere i codici di errore PSDK, gli avvisi e i codici di errore nativi.

## Errori

La tabella seguente fornisce informazioni dettagliate sulle notifiche di tipo ERRORE. La maggior parte degli errori contiene metadati pertinenti; ad esempio, l&#39;URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1">
  <tr> 
   <th><b>Nome errore PSDK</b></th>
   <th><b>Codice errore PSDK</b></th>
   <th><b>Descrizione</b></th>
  </tr>
  <tr>
    <td>SUCCESSO</td>
    <td>0</td>
    <td>L'operazione eseguita dall'API sottostante ha esito positivo.</td>
  </tr>
  <tr>
    <td>INVALID_ARGUMENT</td>
    <td>1</td>
    <td>I dati o il formato dell'argomento fornito all'API sottostante non sono validi.</td>
  </tr>
  <tr>
    <td>NULL_POINTER</td>
    <td>2</td>
    <td>Uno degli argomenti passati è NULL O uno dei membri interni non è stato inizializzato.</td>
  </tr>
  <tr>
    <td>ILLEGAL_STATE</td>
    <td>3</td>
    <td>L'operazione non è supportata nello stato corrente del lettore.</td>
  </tr>
  <tr>
    <td>INTERFACE_NOT_FOUND</td>
    <td>4</td>
    <td>Il metodo interfaceCast genera questo errore quando l'interfaccia richiesta non è implementata/ereditata da questo.</td>
  </tr>
  <tr>  
    <td>CREATION_FAILED</td>
    <td>5</td>
    <td>Creazione di una delle risorse interne non riuscita.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_OPERATION</td>
    <td>6</td>
    <td>Al momento l'operazione richiesta non è supportata.</td>
  </tr>
  <tr>
    <td>DATA_NOT_AVAILABLE</td>
    <td>7</td>
    <td>I dati richiesti non sono attualmente disponibili.</td>
  </tr>
  <tr>
    <td>SEEK_ERROR</td>
    <td>8</td>
    <td>Errore durante l'esecuzione di un'operazione di ricerca.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_FEATURE</td>
    <td>9</td>
    <td>Funzione non supportata.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>10</td>
    <td>Il valore specificato non è compreso nell'intervallo.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>11</td>
    <td>Il codec audio/video del flusso non è supportato da TVSDK o dal dispositivo sottostante.</td>
  </tr>
  <tr>
    <td>MEDIA_ERROR</td>
    <td>12</td>
    <td>Il supporto specificato non è stato trovato.</td>
  </tr>
  <tr>
    <td>NETWORK_ERROR</td>
    <td>13</td>
    <td>Si è verificato un errore durante il download di un frammento o segmento (sia video che audio).</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>14</td>
    <td>Evento di errore generico. Non emesso da TVSDK. Questo è solo un indicatore per la fine dell'intervallo di codici numerici corrispondenti agli eventi di errore TVSDK.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>15</td>
    <td>Il tempo di ricerca specificato non è valido.</td>
  </tr>
  <tr>
    <td>AUDIO_TRACK_ERROR</td>
    <td>16</td>
    <td>Si è verificato un errore relativo a una traccia audio (audio alternativo)</td>
  </tr>
  <tr>
    <td>ACCESS_FROM_DIFFERENT_THREAD</td>
    <td>17</td>
    <td>L'API PSDK viene chiamata da un thread diverso da quello in cui è stato inizializzato PSDK.</td>
  </tr>
  <tr>
    <td>ELEMENT_NOT_FOUND</td>
    <td>18</td>
    <td>L'elemento non è stato trovato.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>19</td>
    <td>Funzionalità non implementata.</td>
  </tr>
  <tr>
    <td>PRE_ROLL_DISABLED</td>
    <td>20</td>
    <td>Il preroll è stato disabilitato tramite AdvertisingMetadata.</td>
  </tr>
  <tr>
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>La riproduzione HLS non è stata abilitata in Flash Player. Consulta AuthorizedFeatures.enableMediaPlayerHLSPlayback().</td>
  </tr>
  <tr>
    <td>NETWORK_TIMEOUT</td>
    <td>58</td>
    <td>Timeout della rete durante il recupero di una risorsa/la connessione a un server.</td>
  </tr>
</table>

## Avvisi

La tabella seguente fornisce informazioni dettagliate sulle notifiche di tipo WARN.
La maggior parte delle avvertenze contiene metadati pertinenti; ad esempio, l&#39;URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Nome errore</b></th>
    <th><b>Code</b></th>
    <th><b>Descrizione</b></th>
  </tr>
  <tr>
    <td>PLAYBACK_OPERATION_FAILED</td>
    <td>200</td>
    <td>Errore durante l'operazione di riproduzione. Operazione relativa alla riproduzione non riuscita</td>
  </tr>
  <tr>  
    <td>NATIVE_WARNING</td>
    <td>201</td>
    <td>Errore della libreria AVE di basso livello.</td>
  </tr>
  <tr>
    <td>AD_RESOLVER_FAILED</td>
    <td>202</td>
    <td>Impossibile risolvere gli annunci.</td>
  </tr>
  <tr>
    <td>AD_MANIFEST_LOAD_FAILED</td>
    <td>203</td>
    <td>Impossibile caricare il manifesto dell'annuncio.</td>
  </tr>
  <tr>
    <td>AD_RESO_IN_PROGRESS</td>
    <td>204</td>
    <td>Operazione per la risoluzione degli annunci è in corso.</td>
  </tr>
  </table>

## Informazioni

<table frame="all" colsep="1" rowsep="1">
  <tr> 
    <th><b>Nome errore</b></th>
    <th><b>Code</b></th>
    <th><b>Descrizione</b></th>
  </tr>
  <tr>
    <td>REVENUE_OPTIMIZATION_REPORTING</td>
    <td>300</td>
    <td>Notifiche dettagliate TVSDK per ulteriori reporting e analisi.</td>
  </tr>
 </table>

## Codici di errore nativi

L&#39;interfaccia Video Encoder di AVE restituisce le notifiche di riproduzione video nell&#39;oggetto metadati NATIVE_ERROR.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Nome errore</b></th>
    <th><b>Code</b></th>
    <th><b>Descrizione</b></th>
  </tr>
  <tr>  
    <td>END_OF_PERIOD</td>
    <td>-1</td>
    <td>Fine del periodo.</td>
  </tr>
  <tr>
    <td>SUCCESSO</td>
    <td>0</td>
    <td>Operazione completata.</td>
  </tr>
  <tr>
    <td>ASYNC_OPERATION_IN_PROGRESS</td>
    <td>1</td>
    <td>Operazione asincrona. La richiesta di operazione è stata effettuata. Le informazioni sul successo/fallimento saranno disponibili in seguito.</td>
  </tr>
  <tr>
    <td>EOF</td>
    <td>2</td>
    <td>Operazione non possibile a causa della condizione di fine del file (EOF).</td>
  </tr>
  <tr>
    <td>DECODER_FAILED</td>
    <td>3</td>
    <td>Il decodificatore non è riuscito in fase di esecuzione.</td>
  </tr>
  <tr>
    <td>DEVICE_OPEN_ERROR</td>
    <td>4</td>
    <td>Impossibile aprire il decodificatore hardware.</td>
  </tr>
  <tr>
    <td>FILE_NOT_FOUND</td>
    <td>5</td>
    <td>Impossibile individuare la risorsa.</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>6</td>
    <td>Errore generico.</td>
  </tr>
  <tr>
    <td>IRRECOVERABLE_ERROR</td>
    <td>7</td>
    <td>Una condizione di errore per la quale il motore video non è in grado di eseguire il ripristino.</td>
  </tr>
  <tr>
    <td>LOST_CONNECTION_RECOVERABLE</td>
    <td>8</td>
    <td>Errore di rete, tentativo di ripristino.</td>
  </tr>
  <tr> 
    <td>NO_FIXED_SIZE</td>
    <td>9</td>
    <td>Impossibile determinare la dimensione della risorsa.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>10</td>
    <td>Funzionalità non implementata.</td>
  </tr>
  <tr>
    <td>OUT_OF_MEMORY</td>
    <td>11</td>
    <td>Memoria insufficiente.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR</td>
    <td>12</td>
    <td>Errore durante l'analisi del file multimediale.</td>
  </tr>
  <tr>  
    <td>SIZE_UNKNOWN</td>
    <td>13</td>
    <td>La risorsa ha una dimensione, ma è sconosciuta.</td>
  </tr>
  <tr>  
    <td>UNDER_FLOW</td>
    <td>14</td>
    <td>Condizione di underflow.</td>
  </tr>
  <tr> 
    <td>UNSUPPORTED_CONFIG</td>
    <td>15</td>
    <td>Configurazione non supportata.</td>
  </tr>
  <tr>  
    <td>UNSUPPORTED_OPERATION</td>
    <td>16</td>
    <td>Operazione non supportata.</td>
  </tr>
  <tr>
    <td>WAITING_FOR_INIT</td>
    <td>17</td>
    <td>Non ancora inizializzato.</td>
  </tr>
  <tr>  
    <td>INVALID_PARAMETER</td>
    <td>18</td>
    <td>Parametro non valido.</td>
  </tr>
  <tr>
    <td>INVALID_OPERATION</td>
    <td>19</td>
    <td>Operazione non consentita.</td>
  </tr>
  <tr>
    <td>OP_ONLY_ALLOWED_IN_PAUSED_STATE</td>
    <td>20</td>
    <td>L'operazione è consentita solo in pausa.</td>
  </tr>
  <tr> 
    <td>OP_INVALID_WITH_AUDIO_ONLY_FILE</td>
    <td>21</td>
    <td>L'operazione non può essere utilizzata solo sui file audio.</td>
  </tr>
  <tr>
    <td>PREVIOUS_STEP_SEEK_IN_PROGRESS</td>
    <td>22</td>
    <td>L'operazione di ricerca precedente è ancora in corso.</td>
  </tr>
  <tr> 
    <td>SOURCE_NOT_SPECIFIED</td>
    <td>23</td>
    <td>Risorsa non specificata.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>24</td>
    <td>Il valore specificato non è compreso nell'intervallo.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>25</td>
    <td>Tempo di ricerca non valido.</td>
  </tr>
  <tr>
    <td>FILE_STRUCTURE_INVALID</td>
    <td>26</td>
    <td>Il file specificato non è conforme alla sintassi prevista.</td>
  </tr>
  <tr>
    <td>COMPONENT_CREATION_FAILURE</td>
    <td>27</td>
    <td>Impossibile creare un componente essenziale.</td>
  </tr>
  <tr>
    <td>DRM_INIT_ERROR</td>
    <td>28</td>
    <td>Impossibile creare il contesto DRM.</td>
  </tr>
  <tr>
    <td>CONTAINER_NOT_SUPPORTED</td>
    <td>29</td>
    <td>Tipo di contenitore non supportato.</td>
  </tr>
  <tr>
    <td>SEEK_FAILED</td>
    <td>30</td>
    <td>Ricerca non riuscita.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>31</td>
    <td>Codec non supportato.</td>
  </tr>
  <tr>
    <td>NETWORK_UNAVAILABLE</td>
    <td>32</td>
    <td>Rete non disponibile.</td>
  </tr>
  <tr>  
    <td>NETWORK_ERROR</td>
    <td>33</td>
    <td>Errore durante il recupero dei dati dalla rete.</td>
  </tr>
  <tr>
    <td>OVERFLOW</td>
    <td>34</td>
    <td>Overflow.</td>
  </tr>
  <tr>  
    <td>VIDEO_PROFILE_NOT_SUPPORTED</td>
    <td>35</td>
    <td>Profilo video non supportato.</td>
  </tr>
  <tr>
    <td>PERIOD_NOT_LOADED</td>
    <td>36</td>
    <td>È stata tentata un'operazione su un periodo HOLD o su un periodo non ancora caricato.</td>
  </tr>
  <tr> 
    <td>INVALID_REPLACE_DURATION</td>
    <td>37</td>
    <td>La durata di sostituzione specificata non è valida o si estende oltre la fine del flusso.</td>
  </tr>
  <tr>
    <td>CALLED_FROM_WRONG_THREAD</td>
    <td>38</td>
    <td>L'API non può essere chiamata dal thread sbagliato. Principalmente, per gli elementi API che dovrebbero essere richiamati solo dal thread principale.</td>
  </tr>
  <tr>
    <td>FRAGMENT_READ_ERROR</td>
    <td>39</td>
    <td>Errore di lettura del frammento. Nessun failover presente. Il motore tenterà di leggere il frammento successivo.</td>
  </tr>
  <tr>
    <td>ABORTO</td>
    <td>40</td>
    <td>L'operazione è stata interrotta da una chiamata Abort o Destroy esplicita.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_HLS_VERSION</td>
    <td>41</td>
    <td>Impossibile riprodurre questa versione del supporto HLS.</td>
  </tr>
  <tr>
    <td>CANNOT_FAIL_OVER</td>
    <td>42</td>
    <td>Impossibile eseguire il failover.</td>
  </tr>
  <tr> 
    <td>HTTP_TIME_OUT</td>
    <td>43</td>
    <td>Timeout del download HTTP.</td>
  </tr>
  <tr>
    <td>NETWORK_DOWN</td>
    <td>44</td>
    <td>La connessione di rete dell'utente non è attiva. La riproduzione potrebbe arrestarsi in qualsiasi momento e riprenderà quando la connessione sarà disponibile.</td>
  </tr>
  <tr>
    <td>NO_USABLE_BITRATE_PROFILE</td>
    <td>45</td>
    <td>Nessun profilo di bitrate utilizzabile trovato nel flusso.</td>
  </tr>
  <tr>
    <td>BAD_MANIFEST_SIGNATURE</td>
    <td>46</td>
    <td>Il manifesto ha una firma errata. Il test di firma del manifesto non è riuscito.</td>
  </tr>
  <tr>
    <td>CANNOT_LOAD_PLAYLIST</td>
    <td>47</td>
    <td>Impossibile caricare una playlist.</td>
  </tr>
  <tr>
    <td>REPLACEMENT_FAILED</td>
    <td>48</td>
    <td>La sostituzione specificata in un'API Insert non è riuscita. Ciò significa che l'inserimento è riuscito ma non è stato sostituito. La sostituzione potrebbe non riuscire se il manifesto da sostituire è stato rimosso dalla timeline.</td>
  </tr>
  <tr>
    <td>SWITCH_TO_ASYMMETRIC_PROFILE</td>
    <td>49</td>
    <td>DRM sta passando a un profilo asimmetrico. Tutti i profili devono essere allineati in base alla durata. In caso contrario, l'avviso verrà visualizzato e potrebbero verificarsi salti durante la riproduzione.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_BACKWARD</td>
    <td>50</td>
    <td>La finestra Live deve essere spostata solo in avanti. In caso contrario, verrà visualizzato questo avviso e la finestra non verrà letta. A causa di ciò, durante la riproduzione potrebbero verificarsi salti (o interruzioni/pause lunghe).</td>
  </tr>
  <tr>
    <td>CURRENT_PERIOD_EXPIRED</td>
    <td>51</td>
    <td>La finestra Live si è spostata oltre il periodo corrente.</td>
  </tr>
  <tr>
    <td>CONTENT_LENGTH_MISMATCH</td>
    <td>52</td>
    <td>La lunghezza del contenuto indicata dal server HTTP non corrisponde alla dimensione effettiva del supporto.</td>
  </tr>
  <tr>
    <td>PERIOD_HOLD</td>
    <td>53</td>
    <td>Il lettore multimediale non è in grado di leggere ulteriormente perché ha raggiunto il tempo impostato dall'API setHoldAt.</td>
  </tr>
  <tr>  
    <td>LIVE_HOLD</td>
    <td>54</td>
    <td>Il lettore multimediale non è in grado di caricare i segmenti perché ha raggiunto la fine della finestra dal vivo. Il caricamento del segmento riprenderà quando il server aggiungerà nuovi supporti alla finestra dal vivo. Questo stato viene generalmente raggiunto se:<ul><li>Il valore bufferTime è troppo alto (uguale o superiore alla durata della finestra attiva).</li><li>Una combinazione di una o più API insert/delete ha sostituito più supporti rispetto a quelli aggiunti.</li><li>Il periodo successivo è un periodo live con una sostituzione di supporti in sospeso (a causa della chiamata API InsertBy)</li></ul></td>
  </tr>
  <tr>
    <td>BAD_MEDIA_INTERLEAVING</td>
    <td>55</td>
    <td>L'interfoliazione audio e video nel supporto non viene eseguita correttamente. Si tratta di un errore di package. L'avviso viene inviato quando la differenza supera i due secondi.</td>
  </tr>
  <tr>
    <td>DRM_NOT_AVAILABLE</td>
    <td>56</td>
    <td></td>
  </tr>
  <tr>  
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>La riproduzione HLS non è stata abilitata in Flash Player. Consulta AuthorizedFeatures.enableHLSPlayback.</td>
  </tr>
  <tr>
    <td>BAD_MEDIA_SAMPLE_FOUND</td>
    <td>58</td>
    <td>Il decodificatore ha ricevuto un campione errato che non può essere decodificato. In genere non si tratta di un errore fatale, ma indica che potrebbero verificarsi dei problemi nell’audio/video. Troppe istanze di questo errore indicano una codifica non valida o un file non valido.</td>
  </tr>
  <tr>
    <td>RANGE_SPANS_READ_HEAD</td>
    <td>59</td>
    <td>Dopo l'avvio della riproduzione, l'intervallo Inserisci/Sostituisci non deve contenere la testina di lettura.</td>
  </tr>
  <tr> 
    <td>POSTROLL_WITH_LIVE_NOT_ALLOWED</td>
    <td>60</td>
    <td>Gli inserimenti post-roll non sono consentiti su un supporto live. Tuttavia, sono consentiti dopo che il server contrassegna il supporto come completo.</td>
  </tr>
  <tr>
    <td>INTERNAL_ERROR</td>
    <td>61</td>
    <td>Una questione molto rara che non dovrebbe mai accadere.</td>
  </tr>
  <tr>  
    <td>SPS_PPS_FOUND_OUTSIDE_AVCC</td>
    <td>62</td>
    <td>Il flusso non segue la raccomandazione del package di inserire sempre H264 SPS/PPS in un AVCC. È possibile che si verifichino problemi di ricerca/riproduzione.</td>
  </tr>
  <tr>  
    <td>PARAL_REPLACEMENT</td>
    <td>63</td>
    <td>La sostituzione specificata in un'API Insert è stata eseguita solo in parte. Questo accade quando replaceDuration si estende sulla durata della timeline.</td>
  </tr>
  <tr>
    <td>RENDITION_M3U8_ERROR</td>
    <td>64</td>
    <td>Errore durante il caricamento della playlist della rappresentazione. Questo è solo per AVE, non per Flash Player.</td>
  </tr>
  <tr>
    <td>NULL_OPERATION</td>
    <td>65</td>
    <td>L'operazione non ha alcun effetto.</td>
  </tr>
  <tr>
    <td>SEGMENT_SKIPPED_ON_FAILURE</td>
    <td>66</td>
    <td>Il segmento non può essere riprodotto e viene ignorato in caso di errore.</td>
  </tr>
  <tr>
    <td>INCOMPATIBLE_RENDER_MODE</td>
    <td>67</td>
    <td>Modalità di rendering non compatibile.</td>
  </tr>
  <tr>
    <td>PROTOCOL_NOT_SUPPORTED</td>
    <td>68</td>
    <td>Il protocollo Web utilizzato nell'URL non è supportato.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR_INCOMPATIBLE_VERSION</td>
    <td>69</td>
    <td>Errore durante l'analisi del file multimediale.</td>
  </tr>
  <tr>  
    <td>MANIFEST_FILE_UNEXPECTEDLY_CHANGED</td>
    <td>70</td>
    <td>Il file manifesto è stato modificato in modo imprevisto.</td>
  </tr>
  <tr>
    <td>CANNOT_SPLIT_TIMELINE</td>
    <td>71</td>
    <td>Impossibile eseguire un'operazione di divisione su una timeline.</td>
  </tr>
  <tr>
    <td>CANNOT_ERASE_TIMELINE</td>
    <td>72</td>
    <td>Impossibile eseguire un'operazione di cancellazione su una timeline.</td>
  </tr>
  <tr>
    <td>DID_NOT_GET_NEXT_FRAGMENT</td>
    <td>73</td>
    <td>Impossibile ottenere il frammento successivo.</td>
  </tr>
  <tr>
    <td>NO_TIMELINE</td>
    <td>74</td>
    <td>Nessuna timeline presente in una struttura dati interna.</td>
  </tr>
  <tr>
    <td>LISTENER_NOT_FOUND</td>
    <td>75</td>
    <td>Nessun listener trovato in una struttura dati interna.</td>
  </tr>
  <tr>
    <td>AUDIO_START_ERROR</td>
    <td>76</td>
    <td>Impossibile avviare l'audio.</td>
  </tr>
  <tr>
    <td>NO_AUDIO_SINK</td>
    <td>77</td>
    <td>Nessun lavello audio presente in una struttura dati interna.</td>
  </tr>
  <tr>  
    <td>FILE_OPEN_ERROR</td>
    <td>78</td>
    <td>Impossibile aprire il file.</td>
  </tr>
  <tr>
    <td>FILE_WRITE_ERROR</td>
    <td>79</td>
    <td>Impossibile scrivere in un file.</td>
  </tr>
  <tr>
    <td>FILE_READ_ERROR</td>
    <td>80</td>
    <td>Impossibile leggere da un file.</td>
  </tr>
  <tr>
    <td>ID3PARSE_ERROR</td>
    <td>81</td>
    <td>Errore durante l'analisi dei dati ID3.</td>
  </tr>
  <tr>
    <td>SECURITY_ERROR</td>
    <td>82</td>
    <td>Caricamento del contenuto non riuscito a causa di restrizioni di protezione.</td>
  </tr>
  <tr>
    <td>TIMELINE_TOO_SHORT</td>
    <td>83</td>
    <td>La durata della timeline è troppo breve. Se si tratta di un flusso live, possono verificarsi frequenti buffering.</td>
  </tr>
  <tr>
    <td>AUDIO_ONLY_STREAM_START</td>
    <td>84</td>
    <td>Lo streaming è stato commutato in un flusso solo audio.</td>
  </tr>
  <tr>  
    <td>AUDIO_ONLY_STREAM_END</td>
    <td>85</td>
    <td>Lo streaming è stato commutato da solo audio a un flusso con video.</td>
  </tr>
  <tr>
    <td>KEY_NOT_FOUND</td>
    <td>87</td>
    <td>Impossibile trovare la chiave.</td>
  </tr>
  <tr>
    <td>INVALID_KEY</td>
    <td>88</td>
    <td>La chiave non è valida.</td>
  </tr>
  <tr>
    <td>KEY_SERVER_NOT_FOUND</td>
    <td>89</td>
    <td>Il server delle chiavi non restituisce una chiave.</td>
  </tr>
  <tr>
    <td>MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</td>
    <td>90</td>
    <td>Impossibile gestire l'aggiornamento del manifesto principale.</td>
  </tr>
  <tr>
    <td>UNREPORTED_TIME_DISCONTINUITY_FOUND</td>
    <td>91</td>
    <td>Discontinuità dell'ora non segnalata (PTS) trovata.</td>
  </tr>
  <tr>
    <td>UNMATCHED_AV_DISCONTINUITY_FOUND</td>
    <td>92</td>
    <td>Discontinuità audio e video non corrispondente rilevata.</td>
  </tr>
  <tr>
    <td>TRICKPLAY_ENDED_DUE_TO_ERROR</td>
    <td>93</td>
    <td>Si è verificato un errore durante la riproduzione del file multimediale in modalità di riproduzione trucco. La modalità di riproduzione dei mattoni è terminata e il flusso viene messo in pausa. Chiamate Play() per riprodurre il supporto in modalità normale.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_AHEAD</td>
    <td>95</td>
    <td>Il giocatore è fuori dalla finestra dal vivo e deve cercare di recuperare.</td>
  </tr>
</table>
