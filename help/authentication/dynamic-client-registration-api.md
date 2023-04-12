---
title: API di registrazione client dinamica
description: API di registrazione client dinamica
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# API di registrazione client dinamica {#dynamic-client-registration-api}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Attualmente, esistono due modi in cui Primetime Authentication identifica e registra le applicazioni:

* i client basati su browser sono registrati tramite [elenco di domini](/help/authentication/programmer-overview.md)
* i client dell&#39;applicazione nativa, come le applicazioni iOS e Android, vengono registrati tramite il meccanismo di richiesta firmato.

Adobe Primetime Authentication propone un nuovo meccanismo per la registrazione delle applicazioni. Questo meccanismo è descritto nei paragrafi seguenti.

## Meccanismo di registrazione delle applicazioni {#appRegistrationMechanism}

### Motivi tecnici {#reasons}

Il meccanismo di autenticazione nell’autenticazione di Adobe Primetime si basava sui cookie di sessione, ma a causa di [Schede personalizzate Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}Questo obiettivo non può più essere raggiunto.

Date queste limitazioni, l&#39;Adobe introduce un nuovo meccanismo di registrazione per tutti i suoi clienti. Si basa sulla RFC OAuth 2.0 e prevede i seguenti passaggi:

1. Recupero dell&#39;istruzione software dal dashboard TVE
1. Recupero delle credenziali client
1. Ottenimento del token di accesso

### Recupero dell&#39;istruzione software dal dashboard TVE {#softwareStatement}

Per ogni applicazione rilasciata, è necessario ottenere un&#39;istruzione software. Tutte le istruzioni software vengono fornite tramite TVE Dashboard, una volta create le applicazioni. L&#39;istruzione software deve essere distribuita insieme all&#39;applicazione sul dispositivo dell&#39;utente.

>[!IMPORTANT]
>
>Quando si utilizza un&#39;istruzione software, il meccanismo requestor id firmato non sarà più necessario.

Per ulteriori dettagli su come creare istruzioni software, visitare il sito [Registrazione client nel dashboard TVE](/help/authentication/dynamic-client-registration.md).

### Recupero delle credenziali client {#clientCredentials}

Dopo aver recuperato un&#39;istruzione software da TVE Dashboard, è necessario registrare l&#39;applicazione con il server di autorizzazione Adobe Primetime. Esegui questa operazione eseguendo una chiamata /register e recuperando l&#39;identificativo client univoco.

**Richiesta**

| chiamata HTTP |  |
|-----------|--------------------|
| path | /o/client/register |
| metodo | POST |

| field |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| software_statement | Istruzione software creata in TVE Dashboard. | obbligatorio |
| redirect_uri | URI utilizzato dall&#39;applicazione per completare il flusso di autenticazione. | facoltativo |

| intestazioni richieste |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| Content-Type | application/json | obbligatorio |
| X-Device-Info | Informazioni sul dispositivo come definito in Passaggio di informazioni sul dispositivo e sulla connessione | obbligatorio |
| Agente utente | Agente utente | obbligatorio |

**Risposta**

| intestazioni di risposta |  |  |
|------------------|------------------|-----------|
| Content-Type | application/json | obbligatorio |

| campi di risposta |  |  |
|---------------------|-----------------|----------------------------|
| client_id | Stringa | obbligatorio |
| client_secret | Stringa | obbligatorio |
| client_id_sent_at | long | obbligatorio |
| redirect_uris | elenco delle stringhe | obbligatorio |
| Grant_types | elenco delle stringhe<br/> **valore accettato**<br/> `client_credentials`: Utilizzato da client non sicuri, ad esempio Android SDK. | obbligatorio |
| errore | **valori accettati**<ul><li>request_non valido</li><li>valid_redirect_uri</li><li>istruzione_software non valida</li><li>unapprovato_software_statement</li></ul> | obbligatorio in un flusso di errore |


#### Risposta di errore {#error-response}

In caso di errore, il server di registrazione risponde con un codice di stato HTTP 400 (Bad Request) e include i seguenti parametri all&#39;interno della risposta:

| codice di stato | organismo di risposta | descrizione |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;: &quot;nome_richiesta non valido&quot;} | Nella richiesta manca un parametro obbligatorio, include un valore di parametro non supportato, ripete un parametro o in caso contrario è errato. |
| HTTP 400 | {&quot;error&quot;: &quot;non valido_redirect_uri&quot;} | Redirect_uri non consentito per questo client in base alla sua applicazione registrata. |
| HTTP 400 | {&quot;error&quot;: &quot;non valido_software_statement&quot;} | Istruzione software non valida. |
| HTTP 400 | {&quot;error&quot;: &quot;unapprovato_software_statement&quot;} | Impossibile trovare software_id nella configurazione. |

#### Esempio di credenziali client {#client-credentials-example}

**Richiesta:**

```HTTPS
POST /o/client/register HTTP/1.1
    User-Agent: Android
    X-Device-Info: ew0KICAibW9kZWwiOiAiVFYiLA0KICAidmVuZG9yIjogIkFwcGxlIiwNCiAgIm1hbnVmYWN0dXJlciI6ICJBcHBsZSIsDQogICJvc05hbWUiOiAidHZPUyIsDQogICJvc1ZlbmRvciI6ICJBcHBsZSIsDQogICJvc1ZlcnNpb24iOiAiMTAuMiIsDQogICJicm93c2VyVmVuZG9yIjogIkFwcGxlIiwNCiAgImJyb3dzZXJOYW1lIjogIlNhZmFyaSINCn0
    Content-Type: application/json
    Accept: application/json
    Host: sp.auth.adobe.com
 {
        "software_statement": "eyJhbGciOiJSUzI1NiJ9.
    eyJzb2Z0d2FyZV9pZCI6IjROUkIxLTBYWkFCWkk5RTYtNVNNM1IiLCJjbGll
    bnRfbmFtZSI6IkV4YW1wbGUgU3RhdGVtZW50LWJhc2VkIENsaWVudCIsImNs
    aWVudF91cmkiOiJodHRwczovL2NsaWVudC5leGFtcGxlLm5ldC8ifQ.
    GHfL4QNIrQwL18BSRdE595T9jbzqa06R9BT8w409x9oIcKaZo_mt15riEXHa
    zdISUvDIZhtiyNrSHQ8K4TvqWxH6uJgcmoodZdPwmWRIEYbQDLqPNxREtYn0
    5X3AR7ia4FRjQ2ojZjk5fJqJdQ-JcfxyhK-P8BAWBd6I2LLA77IG32xtbhxY
    fHX7VhuU5ProJO8uvu3Ayv4XRhLZJY4yKfmyjiiKiPNe-Ia4SMy_d_QSWxsk
    U5XIQl5Sa2YRPMbDRXttm2TfnZM1xx70DoYi8g6czz-CPGRi4SW_S2RKHIJf
    IjoI3zTJ0Y2oe0_EJAiXbL6OyF9S5tKxDXV8JIndSA",
  "redirect_uri": "adobepass://com.programmer"  }
```

**Risposta:**

```HTTPS
HTTP/1.1 201 Created
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
    
{
 "client_id": "s6BhdRkqt3",
 "client_secret": "t7AkePiru4",
 "client_id_issued_at": 2893256800,
 "redirect_uris": [
   "app://com.programmer.adobe#sdasdsadas"],
 "grant_types": ["client_credentials"]
}
```

**Risposta di errore:**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### Ottenimento del token di accesso {#accessToken}

Dopo aver recuperato l’identificatore client univoco (ID client e segreto client) per l’applicazione, devi ottenere un token di accesso. Il token di accesso è un token OAuth 2.0 obbligatorio, utilizzato per chiamare le API di autenticazione di Primetime.

>[!NOTE]
>
>Attualmente, i token di accesso hanno 24 ore di tempo per vivere.

**Richiesta**


| **chiamata HTTP** |  |
| --- | --- |
| path | `/o/client/token` |
| metodo | POST |

| **parametri di richiesta** |  |
| --- | --- |
| `grant_type` | Ricevuto nel processo di registrazione del client.<br/> **Valore accettato**<br/>`client_credentials`: Utilizzato per client non sicuri, come l&#39;SDK per Android. |
| `client_id` | Identificatore client ottenuto nel processo di registrazione client. |
| `client_secret` | Identificatore client ottenuto nel processo di registrazione client. |

**Risposta**

| campi di risposta |  |  |
| --- | --- | --- |
| `access_token` | Il valore del token di accesso da utilizzare per chiamare le API Primetime | obbligatorio |
| `expires_in` | Tempo in secondi fino alla scadenza di access_token | obbligatorio |
| `token_type` | Tipo del token **portatore** | obbligatorio |
| `created_at` | Ora del problema del token | obbligatorio |
| **intestazioni di risposta** |  |  |
| `Content-Type` | application/json | obbligatorio |

**Risposta di errore**

In caso di errore, il server di autorizzazione risponde con un codice di stato HTTP 400 (Bad Request) e include i seguenti parametri all&#39;interno della risposta:

| codice di stato | organismo di risposta | descrizione |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;: &quot;nome_richiesta non valido&quot;} | Nella richiesta manca un parametro obbligatorio, include un valore di parametro non supportato (diverso dal tipo di sovvenzione), ripete un parametro, include più credenziali, utilizza più di un meccanismo di autenticazione del client o è altrimenti in formato non valido. |
| HTTP 400 | {&quot;error&quot;: &quot;client_non valido&quot;} | Autenticazione client non riuscita. Client sconosciuto. L&#39;SDK DEVE registrarsi nuovamente con il server di autorizzazione. |
| HTTP 400 | {&quot;error&quot;: &quot;unauthorized_client&quot;} | Il client autenticato non è autorizzato a utilizzare questo tipo di concessione dell&#39;autorizzazione. |

#### Esempio di ottenimento del token di accesso: {#obt-access-token}

**Richiesta:**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**Risposta:**

```JSON
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"bearer",
  "expires_in":3600,
  "created_at":123456789
}
```

**Risposta di errore:**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## Esecuzione di richieste di autenticazione {#autheticationRequests}

Utilizza il token di accesso per eseguire Adobe Primetime [Chiamate API di autenticazione](/help/authentication/initiate-authentication.md). Per eseguire questa operazione, è necessario aggiungere il token di accesso alla richiesta API, in uno dei seguenti modi:

* aggiungendo un nuovo parametro di query alla richiesta. Viene chiamato il nuovo parametro **access_token**.

* aggiungendo una nuova intestazione HTTP alla richiesta: Autorizzazione: Portatore. È consigliabile utilizzare l’intestazione HTTP , in quanto le stringhe di query tendono a essere visibili nei registri del server.

In caso di errore, è possibile restituire le seguenti risposte di errore:

| Risposte di errore |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| request_non valido | 400 | Richiesta non valida. |
| client_non valido | 403 | L’ID client non è più autorizzato a eseguire richieste. È necessario generare nuove credenziali client. |
| access_negato | 401 | Access_token non valido (scaduto o non valido). Il client DEVE richiedere un nuovo access_token. |

### Esecuzione di esempi di richieste di autenticazione:

**Invio del token di accesso come parametro della richiesta:**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**Invio del token di accesso come intestazione HTTP:**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**Risposte di errore come corpo della risposta:**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**Risposte di errore come parametri URL:**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
