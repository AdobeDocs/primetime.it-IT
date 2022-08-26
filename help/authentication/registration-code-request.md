---
title: Pagina di registrazione
description: Pagina di registrazione
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Pagina di registrazione {#registration-page}

## Endpoint API REST {#clientless-endpoints}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

&lt;reggie_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Descrizione {#create-reg-code-svc}

Restituisce il codice di registrazione generato in modo casuale e l’URI della pagina di accesso.

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametro | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestor}/regcode</br>Ad esempio:</br>REGGIE_FQDN/reggie/v1/sampleRequestorId/regcode | App in streaming</br>o</br>Servizio programmatore | 1. richiedente  </br>    (componente Percorso)</br>2.  deviceId (Hashed)   </br>    (Obbligatorio)</br>3.  device_info/X-Device-Info (obbligatorio)</br>4.  mvpd (facoltativo)</br>5.  ttl (facoltativo)</br>6.  _deviceType_</br> 7.  _deviceUser_ (Obsoleto)</br>8.  _appId_ (Obsoleto) | POST | XML o JSON contenente un codice di registrazione e informazioni o dettagli di errore in caso di errore. Vedi gli schemi e gli esempi seguenti. | 201 |

{style=&quot;table-layout:auto&quot;}

| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| device_info/</br>X-Device-Info | Informazioni sul dispositivo in streaming.</br>**Nota**: QUESTO PUÒ essere passato a device_info come parametro URL, ma a causa della dimensione potenziale di questo parametro e delle limitazioni della lunghezza di un URL GET, DEVE essere passato come X-Device-Info nell&#39;intestazione http. </br>Vedi tutti i dettagli in [Trasferimento delle informazioni sul dispositivo e sulla connessione](http://tve.helpdocsonline.com/passing-device-information). |
| mvpd | ID MVPD per il quale l&#39;operazione è valida. |
| ttl | Quanto tempo deve vivere questo regcode in secondi.</br>**Nota**: Il valore massimo consentito per ttl è di 36000 secondi (10 ore). Valori più elevati generano una risposta HTTP 400 (richiesta errata). Se `ttl` viene lasciata vuota, l’autenticazione Primetime imposta un valore predefinito di 30 minuti. |
| _deviceType_ | Tipo di dispositivo (ad esempio Roku, PC).</br>Se questo parametro è impostato correttamente, ESM offre metriche che [suddivisi per tipo di dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.</br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**Nota**: il parametro device_info sostituirà questo parametro. |
| _deviceUser_ | Identificatore utente del dispositivo. |
| _appId_ | ID/nome dell&#39;applicazione. </br>**Nota**: device_info sostituisce questo parametro. |

{style=&quot;table-layout:auto&quot;}


>[!CAUTION]
>
>**Indirizzo IP del dispositivo di streaming**
></br>
>Per le implementazioni da client a server, l&#39;indirizzo IP del dispositivo di streaming viene inviato in modo implicito con questa chiamata.  Per le implementazioni server-to-server, dove **regcode** La chiamata è effettuata come Servizio programmatore e non come Dispositivo streaming, per trasmettere l&#39;indirizzo IP del dispositivo streaming è necessaria la seguente intestazione:
>
>
>
```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>dove `<streaming\_device\_ip>` è l&#39;indirizzo IP pubblico del dispositivo di streaming.
></br></br>
>Esempio :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1</br>X-Forwarded-For:203.45.101.20
>```
</br>

### Schema XML di risposta {#xml-schema}


#### Codice di registrazione XSD {#registration-code-xsd}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>
```

 </br>

| Nome elemento | Descrizione |
| --------------- | ------------------------------------------------------------------------------------ |
| id | UUID generato dal servizio di registrazione del codice |
| codice | Codice di registrazione generato dal servizio di registrazione |
| richiedente | ID richiedente |
| mvpd | ID Mvpd |
| generato | Timestamp di creazione del codice di registrazione (in millisecondi dal 1° gennaio 1970 GMT) |
| scadenza | Timestamp della scadenza del codice di registrazione (in millisecondi dal 1° gennaio 1970 GMT) |
| deviceId | ID dispositivo univoco (o token XSTS) |
| deviceType | Tipo di dispositivo |
| deviceUser | Utente connesso al dispositivo |
| appId | ID applicazione |
| appVersion | Versione applicazione |
| registerURL | URL dell’app Web di accesso da visualizzare all’utente finale |

{style=&quot;table-layout:auto&quot;}
 </br>

 

### Messaggio di errore XSD  {#error-message}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="rest.pass.adobe.com"
               targetNamespace="rest.pass.adobe.com"
               attributeFormDefault="unqualified"
               elementFormDefault="unqualified">
        <xs:element name="error">
            <xs:complexType>
                <xs:all>
                    <xs:element name="status" type="xs:int" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="message" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="details" type="xs:string" minOccurs="0" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
    </xs:schema>
```
 

### Risposta di esempio {#sample-response}

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```
 
**JSON:**

```JSON
    {
        "id": "678f9fea-9d364b29-246c-488f-b97e-298566d1b9e0",
        "code": "D4BDU2W",
        "requestor": "sampleRequestorId",
        "mvpd": "sampleMvpdId",
        "generated": 1348039555877,
        "expires": 1348043155877,
        "info": {
            "deviceId": "dGhpc0l.kQUR1bW15RGV2.aWNlSWQ=",
            "deviceType": "xboxOne",
            "deviceUser": "JD",
            "appId": "2345",
            "appVersion": "2.0",
            "registrationURL": "http://loginwebapp.com"
        }
    }
```

[Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
