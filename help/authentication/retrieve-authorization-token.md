---
title: Recupera token di autorizzazione
description: Recupera token di autorizzazione
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Recupera token di autorizzazione {#retrieve-authorization-token}

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

Recupera il token di autorizzazione (AuthZ).  


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/token/authz</br></br>Ad esempio:</br></br>&lt;sp_fqdn>/api/v1/token/authz | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente (obbligatorio)</br>2.  deviceId (obbligatorio)</br>3.  risorsa (obbligatoria)</br>4.  device_info/X-Device-Info (obbligatorio)</br>5.  _deviceType_</br> 6.  _deviceUser_ (Obsoleto)</br>7.  _appId_ (Obsoleto) | GET | 1. Completato</br>2.  Token di autenticazione  </br>    non trovato o scaduto:   </br>    Motivo della spiegazione XML  </br>    token di autenticazione non trovato</br>3.  Token di autorizzazione  </br>    non trovato:  </br>    Spiegazione XML</br>4.  Token di autorizzazione  </br>    scaduto:  </br>    Spiegazione XML | 200 - Successo  </br>412 - No AuthN</br></br>404 - No AuthZ</br></br>410 - AuthZ scaduto |

{style=&quot;table-layout:auto&quot;}

</br>

| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| risorsa | Una stringa che contiene un resourceId (o frammento MRSS), identifica il contenuto richiesto da un utente ed è riconosciuta dagli endpoint di autorizzazione MVPD. |
| device_info/</br></br>X-Device-Info | Informazioni sul dispositivo in streaming.</br></br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br></br>Vedi tutti i dettagli in [Trasferimento delle informazioni sul dispositivo e sulla connessione](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br></br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Nota**: il parametro device_info sostituirà questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo. |
| _appId_ | ID/nome dell&#39;applicazione. </br></br>**Nota**: device_info sostituisce questo parametro. |

{style=&quot;table-layout:auto&quot;}


### Risposta di esempio {#response}

 

#### Completato

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
        <expires>1348148289000</expires>
        <mvpd>sampleMvpdId</mvpd>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <proxyMvpd>sampleProxyMvpdId</proxyMvpd>
    </authorization>
```

 

**JSON:**

```JSON
    {
        "mvpd": "sampleMvpdId",
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348148289000",
        "proxyMvpd": "sampleProxyMvpdId"
    }
```

 </br>


#### Token di autenticazione non trovato o scaduto:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>412</status>
        <message>User not authenticated</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 412,
        "message": "User not authenticated",
        "details": null
    }
```

</br>
 

#### Token di autorizzazione non trovato:

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
        "message": "Not Found",
        "details": null
    }
```

</br>

 

#### Token di autorizzazione scaduto:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>410</status>
        <message>Gone</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 410,
        "message": "Gone",
        "details": null
    }
```

[Torna a Clientless API Reference](http://tve.helpdocsonline.com/clientless-api-reference)
