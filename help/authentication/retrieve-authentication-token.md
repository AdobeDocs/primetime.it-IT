---
title: Recupera token di autenticazione
description: Recupera token di autenticazione
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Recupera token di autenticazione {#retrieve-authentication-token}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Endpoint API REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descrizione {#description}

Recupera il token di autenticazione (AuthN).  

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/token/autenticazione</br></br>Ad esempio:</br></br>&lt;sp_fqdn>/api/v1/token/autenticazione | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente (obbligatorio)</br>2.  deviceId (obbligatorio)</br>3.  device_info/X-Device-Info (obbligatorio)</br>4.  _deviceType_ (obsoleto)</br>5.  _deviceUser_ (Obsoleto)</br>6.  _appId_ (Obsoleto) | GET | XML o JSON contenente informazioni di autenticazione o dettagli di errore in caso di esito negativo. | 200 - Successo.  </br>404 - Token non trovato  </br>410 - Token scaduto |

{style=&quot;table-layout:auto&quot;}


| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br>Vedi tutti i dettagli in [Trasferimento delle informazioni sul dispositivo e sulla connessione](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>**Nota**: device_info sostituisce questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo.</br></br>**Nota**: se utilizzato, deviceUser deve avere gli stessi valori di nel [Crea codice di registrazione](http://tve.helpdocsonline.com/registration-code-request) richiesta. |
| _appId_ | ID/nome dell&#39;applicazione. </br></br>**Nota**: device_info sostituisce questo parametro. Se utilizzato, `appId` deve avere gli stessi valori di nel [Crea codice di registrazione](http://tve.helpdocsonline.com/registration-code-request) richiesta. |

{style=&quot;table-layout:auto&quot;}

</br>

### Risposta di esempio {#response}

 

#### Completato

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authentication>
         <expires>1601114932000</expires>
         <userId>sampleUserId</userId>
         <mvpd>sampleMvpdId</mvpd>
         <requestor>sampleRequestor</requestor>
    </authentication>
```


**JSON:**

```JSON
    {
         "requestor": "sampleRequestor",
         "mvpd": "sampleMvpdId",
         "userId": "sampleUserId",
         "expires": "1601114932000"
    }
```

 

 

#### Token di autenticazione non trovato:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>404</status>
        <message>Not found</message>
    </error>
```

 
**JSON:**

```JSON
    {
        "status": 404,
        "message": "Not Found"
    }
```

[Torna a Clientless API Reference](http://tve.helpdocsonline.com/clientless-api-reference)
