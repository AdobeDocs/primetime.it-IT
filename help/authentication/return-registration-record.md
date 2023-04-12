---
title: Record di registrazione del ritorno
description: Record di registrazione del ritorno
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Record di registrazione del ritorno {#return-registration-record}

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

Restituisce il record del codice di registrazione contenente UID del codice di registrazione, codice di registrazione e ID dispositivo con hash. 

 

<div>


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Ad esempio:</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJCFK?format=xml | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente  </br>    (componente Percorso)</br>2.  codice di registrazione  </br>    (componente Percorso) | GET | XML o JSON contenente un codice di registrazione e informazioni. Vedi schema ed esempio di seguito. | 200 |

{style="table-layout:auto"}

</br>

| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| codice di registrazione | Il valore del codice di registrazione che verrà visualizzato sul dispositivo streaming (da immettere nel flusso di autenticazione). |

</br>

## Schema XML di risposta {#response-xml-schema}

### Codice di registrazione XSD

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

| Nome elemento | Descrizione |
| --- | --- |
| id | UUID generato dal servizio di registrazione del codice |
| codice | Codice di registrazione generato dal servizio di registrazione |
| richiedente | ID richiedente |
| mvpd | ID MVPD |
| generato | Timestamp di creazione del codice di registrazione (in millisecondi dal 1° gennaio 1970 GMT) |
| scadenza | Timestamp della scadenza del codice di registrazione (in millisecondi dal 1° gennaio 1970 GMT) |
| deviceId | ID dispositivo univoco (o token XSTS) |
| deviceType | Tipo di dispositivo |
| deviceUser | Utente connesso al dispositivo |
| appId | ID applicazione |
| appVersion | Versione applicazione |
| registerURL | URL dell’app Web di accesso da visualizzare all’utente finale |

{style="table-layout:auto"}

### Risposta di esempio {#sample-response}

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
