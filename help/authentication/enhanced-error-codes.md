---
title: Codici di errore migliorati
description: Codici di errore migliorati
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# Codici di errore migliorati {#enhanced-error-codes}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

In questo documento viene descritto l’elenco dei codici di errore API e le informazioni aggiuntive sugli errori restituiti alle applicazioni.

Per utilizzare i codici di errore avanzati nell&#39;applicazione Programmers, è necessario effettuare una richiesta al team di supporto per abilitarlo con una modifica della configurazione.

## Gestione degli errori di risposta {#response-error-handling}

Nella maggior parte degli scenari, l&#39;API di autenticazione Primetime include informazioni di errore aggiuntive nel corpo della risposta per fornire **contesto significativo** perché si è verificato un certo errore e/o possibili soluzioni per risolvere automaticamente il problema.  *Tuttavia, in alcuni casi specifici che coinvolgono flussi di autenticazione o logout, i servizi Primetime Authentication potrebbero restituire una risposta HTML o un corpo vuoto. Per ulteriori informazioni, consulta la documentazione API .*

Mentre alcuni tipi di errori possono essere gestiti automaticamente (ad esempio, riprovando una richiesta di autorizzazione in caso di timeout della rete o richiedendo all&#39;utente di ripetere l&#39;autenticazione se la sessione è scaduta), altri tipi potrebbero richiedere modifiche di configurazione o l&#39;interazione con il team di assistenza clienti. È importante che i programmatori raccolgano e forniscano informazioni complete sugli errori in tali casi.

L&#39;API di autenticazione Primetime restituisce i codici di stato HTTP compresi nell&#39;intervallo 400-500 per indicare errori o errori. Ogni codice di stato HTTP ha alcune implicazioni:

- I codici di errore 4xx implicano che l’errore è generato dal client e che il client deve eseguire ulteriori operazioni per correggerlo (ad esempio, ottenere un token di accesso prima di richiamare le API protette o fornire eventuali parametri richiesti)

- I codici di errore 5xx implicano che l&#39;errore è generato dal server e che il server deve eseguire ulteriori operazioni per correggerlo.

Le informazioni aggiuntive sull’errore sono incluse nel campo &quot;error&quot; all’interno del corpo della risposta. 




| Nome | Tipo | Esempio | Descrizione |
| --- | --- | --- | --- |
| **errore** | _oggetto_ | JSON <br>    {<br>        &quot;status&quot; : 403,<br>        &quot;code&quot; : &quot;network_connection_failed&quot;,<br>        &quot;message&quot; : &quot;Impossibile contattare i servizi del provider TV&quot;,<br>        &quot;helpUrl&quot; : &quot;&quot;,<br>        &quot;trace&quot; : &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;action&quot; : &quot;riprovare&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | Una raccolta o oggetti di errore raccolti durante il tentativo di completare la richiesta. |

</br>

Le API di Adobe Primetime che gestiscono più elementi (API di autorizzazione preventiva, ecc.) potrebbero indicare se l’elaborazione non è riuscita per un particolare elemento ed è riuscita per altri elementi utilizzando informazioni di errore a livello di elemento. In questo caso, il ***&quot;error&quot;*** l&#39;oggetto si trova a livello di elemento e il corpo della risposta potrebbe contenere più ***&quot;errors&quot;*** oggetti : consulta la documentazione API .

</br>

| Esempio con successo parziale ed errore a livello di elemento |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; : &quot;TestStream1&quot;,<br>  &quot;autorizzato&quot;: true <br>}, </br>{ </br>  &quot;id&quot; : &quot;TestStream2&quot;, <br>   &quot;autorizzato&quot;: false, </br>   &quot;error&quot; : { <br> </br>      &quot;status&quot; : 403,<br>      &quot;code&quot; : &quot;network_connection_failed&quot;,<br>      &quot;message&quot; : &quot;Impossibile contattare i servizi del provider TV&quot;,<br>      &quot;details&quot; (dettagli): &quot;&quot;,<br>      &quot;helpUrl&quot; : &quot;&quot;,<br>      &quot;trace&quot; : &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;action&quot; : &quot;riprovare&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

Ogni oggetto di errore ha i seguenti parametri:

| Nome | Tipo | Esempio | Limitato | Descrizione |
|----|----|----|----|--------------|
| Stato | *integer* | 403 | ♦ | Il codice di stato HTTP della risposta come documentato nella RFC 7231 (https://tools.ietf.org/html/rfc7231#section-6) <br> - 400 Richiesta non valida <br> - 400 Richiesta non valida <br> - 400 Richiesta non valida <br> - 401 Non autorizzato <br> - 403 Vietato <br> - 404 Non trovato <br> - 405 Metodo non consentito <br> - Conflitto 409 <br> - 410 Gone <br> - 412 Precondizione non riuscita <br> - 429 Troppe richieste <br> - Errore del server a intervalli 500 <br> - Servizio 503 non disponibile |
| Codice | *string* | network_connection_failed | ♦ | Codice di errore standard di autenticazione di Primetime. Di seguito è riportato l&#39;elenco completo dei codici di errore. |
| message | *string* | Impossibile contattare i servizi del provider TV |  | Messaggio leggibile dall&#39;utente finale. |
| dettagli | *string* | Il pacchetto di abbonamento non include il canale &quot;Live&quot; |  | In alcuni casi un messaggio dettagliato è fornito dagli endpoint di autorizzazione MVPD o dal programmatore attraverso regole di degradazione. <br> <br> Nota che se non è stato ricevuto alcun messaggio personalizzato dai servizi partner, questo campo potrebbe non essere presente nei campi di errore. |
| helpUrl | *url* | &quot;&quot; |  | Un URL che collega a ulteriori informazioni sul motivo di questo errore e sulle possibili soluzioni. <br> <br>  L’URI rappresenta un URL assoluto e non deve essere dedotto dal codice di errore. A seconda del contesto dell’errore, è possibile fornire un URL diverso. Ad esempio, lo stesso codice di errore bad_request genererà URL diversi per i servizi di autenticazione e autorizzazione. |
| traccia | *string* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | Identificatore univoco per questa risposta che può essere utilizzato quando si contatta il supporto per identificare problemi specifici in scenari più complessi. |
| action | *string* | riprovare | ♦ | *Azione raccomandata per rimediare alla situazione:* </br><br> -none - Purtroppo non esiste un&#39;azione predefinita per risolvere questo problema. Questo potrebbe indicare una chiamata non corretta dell&#39;API pubblica </br><br>-configuration - È necessaria una modifica della configurazione tramite il dashboard TVE o contattando il supporto. </br><br>-domanda-registrazione - La domanda deve registrarsi nuovamente. </br><br>-authentication - L&#39;utente deve autenticare o riautenticare. </br><br>-authorization : l’utente deve ottenere l’autorizzazione per la risorsa specifica. </br><br>-degradazione - Si deve applicare una qualche forma di degradazione. </br><br>-riprovare - Il nuovo tentativo della richiesta potrebbe risolvere il problema</br><br>-riprovare-dopo - Se si ripete la richiesta dopo il periodo di tempo indicato, il problema potrebbe essere risolto. |

</br>

**Note:**

- ***Limitato*** column *indica se il rispettivo valore di campo rappresenta un set finito* (ad esempio, codici di stato HTTP esistenti per &quot;*status*&quot; campo). Gli aggiornamenti futuri di questa specifica potrebbero aggiungere valori all&#39;elenco con restrizioni ma non rimuoveranno o modificheranno quelli esistenti. I campi senza restrizioni in genere possono contenere qualsiasi dato, ma potrebbero esserci limitazioni per garantire dimensioni ragionevoli.

- Ogni risposta di Adobe conterrà un &quot;Adobe-Request-Id&quot; che identifica la richiesta del client in tutti i nostri servizi HTTP. &quot;**traccia**&quot; il campo completa questo e dovrebbero essere segnalati insieme. 

## Codici di stato HTTP e codici di errore {#http-status-codes-and-error-codes}

Le incongruenze tra i vari codici di errore e i relativi codici di stato HTTP associati sono dovute ai requisiti di compatibilità con le versioni precedenti degli sdk e delle applicazioni (ad esempio *unknown\_application* restituisce 400 Richiesta non valida mentre *unknown\_software\_statement* rendimenti 401 non autorizzati). La risoluzione di tali incongruenze sarà oggetto di targeting nelle iterazioni future. 
 
## Azioni e codici di errore {#actions-and-error-codes}

Per la maggior parte dei codici di errore, potrebbero essere idonee più azioni come percorsi per risolvere il problema in questione o potrebbero essere necessarie anche più azioni per correggerli automaticamente. Abbiamo scelto di indicare quello con la probabilità più elevata di correggere l&#39;errore. La **azioni** può essere suddiviso in tre categorie:

1. quelli che tentano di correggere il contesto della richiesta (nuovo tentativo, nuovo tentativo dopo) 
1. quelli che tentano di correggere il contesto utente all&#39;interno dell&#39;applicazione (registrazione dell&#39;applicazione, autenticazione, autorizzazione) 
1. quelli che tentano di correggere il contesto di integrazione tra un&#39;applicazione e un provider di identità (configurazione, degradazione)

Per la prima categoria (riprovare e riprovare dopo), è sufficiente ripetere la stessa richiesta per risolvere il problema. Nel caso di API che gestiscono più elementi, l’applicazione deve ripetere la richiesta e includere solo gli elementi con l’azione &quot;riprova&quot; o &quot;riprova dopo&quot;. Per &quot;*riprovare*&quot; azione, un &quot;<u>Riprova dopo</u>&quot; header indica quanti secondi l&#39;applicazione deve attendere prima di ripetere la richiesta.

Per la seconda e la terza categoria, l’implementazione effettiva delle azioni dipende fortemente dalle funzioni dell’applicazione. Ad esempio, &quot;*degradazione*&quot; può essere implementato come &quot;passaggio a 15 minuti passaggi temporanei per consentire agli utenti la riproduzione del contenuto&quot; o come &quot;strumento automatico per applicare la degradazione AUTHN-ALL o AUTHZ-ALL per la sua integrazione con il MVPD specificato&quot;. Simile a &quot;*autenticazione*&quot; può attivare un&#39;autenticazione passiva (autenticazione back-channel) su un tablet e un flusso di autenticazione a schermo intero su televisori collegati. Per questo motivo abbiamo optato per la fornitura di URL completi con schema e tutti i parametri. 

## Codici di errore {#error-codes}

La tabella degli errori riportata di seguito elenca i possibili codici di errore, i messaggi associati e le azioni possibili.

| Azione | Codice di errore | Codice di stato HTTP | Descrizione |
|---|---|---|--------------|
| configurazione | *authorization_deny_by_mvpd* | 403 | L&#39;MVPD ha restituito una decisione di &quot;rifiuto&quot; quando si richiede l&#39;autorizzazione per la risorsa specificata. |
|  | *authorization_deny_by_parental_Controls* | 403 | L&#39;MVPD ha restituito una decisione &quot;Rifiuta&quot; a causa delle impostazioni dei controlli parentali per la risorsa specificata. |
|  | *authorization_negato_da_programmatore* | 403 | La regola di degrado applicata dal programmatore applica una decisione di &quot;Rifiuto&quot; per l&#39;utente corrente. |
|  | *bad_request* | 400 | La richiesta API non è valida o è formata in modo errato. Consulta la documentazione API per determinare i requisiti della richiesta. |
|  | *individualization_service_non disponibile* | 503 | Richiesta non riuscita perché il servizio di personalizzazione non è disponibile. |
|  | *internal_error* | 500 | Richiesta non riuscita a causa di un errore interno del server. |
|  | *non_client_time* | 400 | La data/ora/fuso orario del computer client non è impostata correttamente. Questo porterà probabilmente a errori di autenticazione/autorizzazione. |
|  | *nome_personalizzato_non valido* | 400 | Lo schema personalizzato specificato utilizzato nella registrazione della domanda non è riconosciuto. Controlla la configurazione del dashboard TVE per i valori dello schema personalizzato corretti. |
|  | *valid_domain* | 400 | Il richiedente sta utilizzando un dominio non valido. Tutti i domini utilizzati da un particolare ID richiedente devono essere elencati nella whitelist di Adobe. |
|  | *nome_non valido* | 400 | Richiesta non riuscita perché conteneva un&#39;intestazione non valida. Consulta la documentazione API per determinare quali intestazioni sono valide per la tua richiesta e se ci sono limitazioni per il loro valore. |
|  | *metodo_http non valido* | 405 | Il metodo HTTP associato alla richiesta non è supportato. Consulta la documentazione API per determinare i metodi HTTP supportati per la richiesta. |
|  | *valore_parametro_non valido* | 400 | Richiesta non riuscita perché conteneva un parametro o un valore di parametro non valido. Consulta la documentazione API per determinare quali parametri sono validi per la richiesta e se sono presenti limitazioni per il loro valore. |
|  | *nome_risorsa_non valido* | 400 | Richiesta non riuscita perché è stata utilizzata una risorsa non valida o non valida. Consulta la documentazione API per determinare quanto complesse risorse devono essere codificate per la richiesta e se ci sono limitazioni per il loro valore e/o le loro dimensioni. |
|  | *codice_registrazione non valido | 404 | Il codice di registrazione specificato non è più valido o è scaduto. |
|  | *non_service_configuration* | 500 | Richiesta non riuscita a causa di una configurazione del servizio non corretta. |
|  | *missing_authentication_header* | 400 | Richiesta non riuscita perché non contiene l&#39;intestazione di autenticazione richiesta per l&#39;API specifica. |
|  | *missing_resource_mapping* | 400 | Nessuna mappatura corrispondente per la risorsa specificata. Contatta il supporto per correggere la mappatura richiesta. |
|  | *preauthorization_deny_by_mvpd* | 403 | L&#39;MVPD ha restituito una decisione di &quot;rifiuto&quot; quando si richiede una pre-autorizzazione per la risorsa specificata. |
|  | *preauthorization_negato_da_programmatore* | 403 | Le regole di degradazione applicate dal programmatore impongono una decisione di &quot;rifiuto&quot; per l&#39;utente corrente. |
|  | *registration_code_service_non disponibile* | 503 | Richiesta non riuscita perché il servizio del codice di registrazione non è disponibile. |
|  | *servizio_non disponibile | 503 | Richiesta non riuscita a causa del fatto che il servizio di autenticazione o autorizzazione non è disponibile. |
|  | *access_token_non disponibile* | 400 | Richiesta non riuscita a causa di un errore imprevisto durante il recupero del token di accesso. Controllare la configurazione del dashboard TVE per le istruzioni software disponibili e gli schemi personalizzati registrati. |
|  | *unsupported_client_version* | 400 | Questa versione di Primetime Authentication SDK è troppo vecchia e non è più supportata. Consulta la documentazione API per i passaggi necessari per effettuare l’aggiornamento alla versione più recente. |
|  | *network_required_ssl* | 403 | Si è verificato un problema di connessione SSL per il servizio partner di destinazione. Contattare il team di supporto. |
|  | *too_molti_resources* | 403 | Richiesta di autorizzazione o di preautorizzazione non riuscita perché sono state interrogate troppe risorse. Contatta il team di supporto per configurare correttamente le limitazioni di autorizzazione e preautorizzazione. |
|  | *programmatore_sconosciuto | 400 | Il programmatore o il fornitore di servizi non è riconosciuto. Utilizzare il Dashboard TVE per registrare il programmatore specificato. |
|  | *unknown_application* | 400 | L&#39;applicazione non è riconosciuta. Utilizza il Dashboard TVE per registrare l&#39;applicazione specificata. |
|  | *unknown_integration* | 400 | L&#39;integrazione tra il programmatore e il provider di identità specificato non esiste. Utilizza il Dashboard TVE per creare l&#39;integrazione richiesta. |
|  | *unknown_software_statement* | 401 | L&#39;istruzione software associata al token di accesso non è riconosciuta. Contattare il team di supporto per chiarire lo stato dell&#39;istruzione software. |
| domanda-registrazione | *access_token_expiration* | 401 | Il token di accesso è scaduto. L’applicazione deve aggiornare il token di accesso come indicato nella documentazione API. |
|  | *nome_accesso_token_signature* | 401 | La firma del token di accesso non è più valida. L’applicazione deve aggiornare il token di accesso come indicato nella documentazione API. |
|  | *id_client_non valido* | 401 | L&#39;identificatore client associato non è riconosciuto. L’applicazione deve seguire il processo di registrazione dell’applicazione come indicato nella documentazione API. |
| autenticazione | *authentication_session_expiration* | 410 | La sessione di autenticazione corrente è scaduta. Per continuare, l’utente deve effettuare nuovamente l’autenticazione con un MVPD supportato. |
|  | *authentication_session_missing* | 401 | Impossibile recuperare la sessione di autenticazione associata a questa richiesta. Per continuare, l’utente deve effettuare nuovamente l’autenticazione con un MVPD supportato. |
|  | *authentication_session_invalidate* | 401 | La sessione di autenticazione è stata invalidata dal provider di identità. Per continuare, l’utente deve effettuare nuovamente l’autenticazione con un MVPD supportato. |
|  | *authentication_session_issuers_mismatch | 400 | Richiesta di autorizzazione non riuscita a causa del fatto che l&#39;MVPD indicato per il flusso di autorizzazione è diverso da quello che ha rilasciato la sessione di autenticazione. Per continuare, l&#39;utente deve effettuare nuovamente l&#39;autenticazione con l&#39;MVPD desiderato. |
|  | *authorization_deny_by_hba_Policies* | 403 | L&#39;MVPD ha restituito una decisione di &quot;rifiuto&quot; a causa di criteri di autenticazione basati su casa. L&#39;autenticazione corrente è stata ottenuta utilizzando un HBA (Home-based Authentication Flow), ma il dispositivo non è più a casa quando si richiede l&#39;autorizzazione per la risorsa specificata. Per continuare, l’utente deve effettuare nuovamente l’autenticazione con un MVPD supportato. |
|  | *identity_not_selected_by_mvpd* | 403 | Richiesta di autorizzazione non riuscita a causa del fatto che l&#39;identità utente non è stata riconosciuta dall&#39;MVPD. |
| autorizzazione | *authorization_expiration* | 410 | L&#39;autorizzazione precedente per la risorsa specificata è scaduta. Per continuare, l’utente deve ottenere una nuova autorizzazione. |
|  | *authorization_not_found* | 404 | Nessuna autorizzazione trovata per la risorsa specificata. Per continuare, l’utente deve ottenere una nuova autorizzazione. |
|  | *device_identifier_mismatch* | 403 | L&#39;identificatore dispositivo specificato non corrisponde all&#39;identificazione del dispositivo di autorizzazione. Per continuare, l’utente deve ottenere una nuova autorizzazione. |
| riprovare | **network_connection_failed** | 403 | Errore di connessione con il servizio partner associato. Il nuovo tentativo di richiesta potrebbe risolvere il problema. |
|  | *network_connection_timeout* | 403 | Si è verificato un timeout di connessione con il servizio partner associato. Il nuovo tentativo di richiesta potrebbe risolvere il problema. |
|  | *network_receive_error* | 403 | Errore di lettura durante il recupero della risposta dal servizio partner associato. Il nuovo tentativo di richiesta potrebbe risolvere il problema. |
|  | *maximum_execute_time_superamento* | 403 | Richiesta non completata nel tempo massimo consentito. Il nuovo tentativo di richiesta potrebbe risolvere il problema. |
| riprovare | *too_many_requests* | 429 | Troppe richieste inviate entro un intervallo specificato. L&#39;applicazione può riprovare la richiesta dopo il periodo di tempo suggerito. |
|  | *nome_utente_limite_superato* | 429 | Troppe richieste emesse da un utente specifico entro un intervallo specificato. L&#39;applicazione può riprovare la richiesta dopo il periodo di tempo suggerito. |

