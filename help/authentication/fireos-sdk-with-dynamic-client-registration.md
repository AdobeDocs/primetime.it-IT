---
title: Amazon FireOS SDK con registrazione client dinamica
description: Amazon FireOS SDK con registrazione client dinamica
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---


# Amazon FireOS SDK con registrazione client dinamica {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## <span id=""></span>Introduzione {#Intro}

FireOS AccessEnabler SDK per FireTV è stato modificato per abilitare l&#39;autenticazione senza utilizzare i cookie di sessione. Poiché sempre più browser limitano l’accesso ai cookie, era necessario un altro metodo per consentire l’autenticazione.

**FireOS SDK 3.0.4** sostituisce l&#39;attuale meccanismo di registrazione dell&#39;app basato sull&#39;autenticazione del richiedente firmato ID e cookie di sessione con [Registrazione client dinamica](/help/authentication/dynamic-client-registration.md).
 

## Modifiche API {#API}

### Factory.getInstance

**Descrizione:** Crea un&#39;istanza dell&#39;oggetto Access Enabler. Deve essere presente una singola istanza di Access Enabler per ogni istanza di applicazione.

| Chiamata API: costruttore |
| --- |
| public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        genera AccessEnablerException |

**Disponibilità:** v3.0+

**Parametri:**

- *appContext*: Contesto dell&#39;applicazione Android
- *softwareStatement*: valore ottenuto dal dashboard TVE o *null* se &quot;software\_statement&quot; è impostato in strings.xml
- *redirectUrl* : per le implementazioni FireTV questo parametro deve essere null. Tutte le impostazioni relative a questo attributo verranno ignorate. 

**Note**

- softwareStatement non valido causerà l&#39;inizializzazione di AccessEnabler o la registrazione dell&#39;applicazione per l&#39;autenticazione e l&#39;autorizzazione di Adobe Pass
- il parametro redirectUrl per FireTV è impostato dall&#39;SDK per l&#39;autenticazione adobepass://android.app as viene gestito dall&#39;istanza AccessEnabler univoca.

### setRequestor

**Descrizione:** Stabilisce l&#39;identità del Canale. A ciascun canale viene assegnato un ID univoco al momento della registrazione con Adobe per il sistema di autenticazione Adobe Primetime. Quando si tratta di token SSO e remoti, lo stato di autenticazione può cambiare quando l&#39;applicazione è in background, setRequestor può essere richiamato nuovamente quando l&#39;applicazione viene portata in primo piano per sincronizzarsi con lo stato del sistema (recupera un token remoto se SSO è abilitato o elimina il token locale se nel frattempo si è verificato un logout).

La risposta del server contiene un elenco di MVPD insieme ad alcune informazioni di configurazione collegate all&#39;identità del Canale. La risposta del server viene utilizzata internamente dal codice di Access Enabler . Solo lo stato dell&#39;operazione (ovvero SUCCESS/FAIL) viene presentato all&#39;applicazione tramite il callback setRequestorComplete().

Se la *url* Il parametro non viene utilizzato, la chiamata di rete risultante esegue il targeting dell&#39;URL predefinito del provider di servizi: ambiente di produzione di rilascio Adobe.

Se viene fornito un valore per *url* , la chiamata di rete risultante esegue il targeting di tutti gli URL forniti nel *url* parametro . Tutte le richieste di configurazione vengono attivate simultaneamente in thread separati. Il primo risponditore ha la precedenza quando si compila l&#39;elenco degli MVPD. Per ogni MVPD nell&#39;elenco, Access Enabler ricorda l&#39;URL del provider di servizi associato. Tutte le richieste di adesione successive vengono indirizzate all&#39;URL associato al provider di servizi che è stato abbinato all&#39;MVPD di destinazione durante la fase di configurazione.

| Chiamata API: configurazione richiedente |
| --- |
| public void setRequestor(String requestorId) |

**Disponibilità:** v3.0+

| Chiamata API: configurazione richiedente |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilità:** v3.0+

**Parametri:**

- *requestorID*: ID univoco associato al canale. Passa l&#39;ID univoco assegnato da Adobe al tuo sito la prima volta che ti registri con il servizio di autenticazione Adobe Primetime.
- *url*: Parametro facoltativo; per impostazione predefinita, viene utilizzato il provider di servizi Adobe (http://sp.auth.adobe.com/). Questo array consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). È possibile utilizzarlo per specificare più istanze del provider di servizi di autenticazione Adobe Primetime. In questo modo, l&#39;elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al fornitore di servizi più veloce; cioè, il fornitore che ha risposto per primo e che supporta quel MVPD.

Obsoleto:

- *signedRequestorID*: Una copia del requestor ID con firma digitale con la tua chiave privata. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Callback attivato:** `setRequestorComplete()`

</br>

### disconnessione

**Descrizione:** Utilizza questo metodo per avviare il flusso di logout. La disconnessione è il risultato di una serie di operazioni di reindirizzamento HTTP a causa del fatto che l&#39;utente deve essere disconnesso sia dai server di autenticazione Adobe Primetime che dai server MVPD. Di conseguenza, questo flusso aprirà una finestra ChromeCustomTab per eseguire il logout.

| Chiamata API: avvia il flusso di logout |
| --- |
| public void logout() |

**Disponibilità:** v3.0+

**Parametri:** Nessuno

**Callback attivato:** `setAuthenticationStatus()`

## Flusso di implementazione del programmatore {#Progr}

### **1. Registra applicazione** 

1. Recuperare software\_statement da Adobe Pass ( TVE Dashboard )
1. Esistono due opzioni per passare questi valori all’SDK di Adobe Pass :
   - Aggiungi : 

      ```
      <string name>"software\_statement">[softwarestatement value]</string>
      ```

   - Chiama AccessEnabler.getInstance(appContext,softwareStatement, null)

 

### **2. Configura applicazione**

- a)  setRequestor(requestor\_id) 

   L’SDK eseguirà le seguenti operazioni: 

   - domanda di registrazione: utilizzo **software\_statement**, l’SDK ottiene un **client\_id, client\_secret, client\_id\_issued\_at, reindirizzare\_uris, Grant\_types**. Queste informazioni verranno memorizzate nell&#39;archivio interno dell&#39;applicazione.
   - ottenere **access\_token** utilizzando client\_id, client\_secret e Grant\_type=&quot;client\_credentials&quot; . Questo accesso\_token verrà utilizzato in ogni chiamata effettuata dall&#39;SDK ai server Adobe Pass.

| Risposte di errore del token : |  |  |
|--- | --- | --- |
| HTTP 400 (richiesta non valida) | {&quot;error&quot;: &quot;non valido\_request&quot;} | Nella richiesta manca un parametro obbligatorio, include un valore di parametro non supportato (diverso dal tipo di sovvenzione), ripete un parametro, include più credenziali, utilizza più di un meccanismo di autenticazione del client o è altrimenti in formato non valido. |
| HTTP 400 (richiesta non valida) | {&quot;error&quot;: &quot;non valido\_client&quot;} | Autenticazione client non riuscita. Client sconosciuto. SDK *DEVE* registrarsi nuovamente con il server di autorizzazione. |
| HTTP 400 (richiesta non valida) | {&quot;error&quot;: &quot;non autorizzato\_client&quot;} | Il client autenticato non è autorizzato a utilizzare questo tipo di concessione dell&#39;autorizzazione. |

- nel caso in cui un MVPD richieda l&#39;autenticazione passiva, un WebView si aprirà per eseguire passiva con tale MVPD e si chiuderà quando completo

- b. checkAuthentication()

   - *true* : vai a Autorizzazione
   - *false* : vai a Select MVPD

- c. getAuthentication : l&#39;SDK includerà **access_token** in parametri di chiamata 

   - mvpd ricorda : vai a setSelectedProvider(mvpd\_id)
   - mvpd non selezionato : displayProviderDialog
   - mvpd selezionato : vai a setSelectedProvider(mvpd\_id)

- d. setSelectedProvider

   - L&#39;url di autenticazione mvpd\_id è caricato in ChromeCustomTabs
   - accesso riuscito : delegate.setAuthenticationStatus ( SUCCESS )
   - accesso annullato : reimposta selezione MVPD
   - Lo schema URL è stabilito come &quot;adobepass://android.app&quot; per acquisire quando l’autenticazione è completa

- e. get/checkAuthorization : L&#39;SDK includerà **access\_token **nell&#39;intestazione come autorizzazione: Portatore **access\_token**

- se l’autorizzazione è riuscita, verrà effettuata una chiamata per ottenere il token multimediale

- f. logout : 

   - L&#39;SDK eliminerà il token valido per il richiedente corrente (le autenticazioni ottenute da altre applicazioni e non tramite SSO rimarranno valide)
   - L’SDK aprirà le schede personalizzate di Chrome per raggiungere l’endpoint di logout mvpd\_id. Una volta completate, le schede personalizzate di Chrome verranno chiuse
   - Lo schema URL è stabilito come &quot;adobepass://logout&quot; per acquisire il momento in cui l’uscita è completa
   - logout attiverà un sendTrackingData(new Event(EVENT\_LOGOUT,USER\_NOT\_AUTHENTICATED\_ERROR) e un callback : setAuthenticationStatus(0,&quot;Logout&quot;)

 

**Nota:** poiché ogni chiamata richiede un **access_token**, i possibili codici di errore seguenti vengono gestiti nell’SDK. 

| Risposte di errore |  |  |
|--- | --- | --- |
| request_non valido | 400 | Richiesta non valida. L&#39;SDK dovrebbe interrompere l&#39;esecuzione delle chiamate al server. |
| client_non valido | 403 | L’ID client non è più autorizzato a eseguire richieste. L&#39;sdk DEVE eseguire nuovamente la registrazione client. |
| access_negato | 401 | Access_token non valido. L&#39;sdk DEVE richiedere un nuovo access_token. |

