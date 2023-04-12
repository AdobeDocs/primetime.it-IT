---
title: Scambio metadati contenuti MVPD
description: Scambio metadati contenuti MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Scambio metadati contenuti MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#content-metadat-exchange-overview}

Questa pagina descrive due implementazioni standard utilizzate dall’autenticazione Adobe Primetime per inviare dati strutturati agli MVPDs sulla richiesta di autorizzazione.  I dati strutturati rappresentano la risorsa (il programmatore) che effettua la richiesta e, eventualmente, dati aggiuntivi come la valutazione del contenuto.

Dal lato del programmatore, l’autenticazione Adobe Primetime supporta risorse di dati MRSS strutturate come segue:

1. Il programmatore invia la risorsa come stringa MRSS. L’autenticazione Adobe Primetime non la codifica sul lato client per dispositivi web o nativi. L&#39;MRSS viene inviato come stringa regolare al server di autenticazione Adobe Primetime.
1. Sul lato server, l’MRSS viene convalidato rispetto allo schema predefinito (http://search.yahoo.com/mrss/).  Se la convalida viene superata, l’autenticazione Adobe Primetime estrae le informazioni dai campi MRSS, tra cui:
   * titolo del canale
   * titolo dell&#39;elemento
   * identificatore risorsa
   * valore e tipo di rating
1. I valori estratti dall&#39;MRSS vengono utilizzati per generare la richiesta di autorizzazione che viene trasmessa all&#39;MVPD.

L’autenticazione Adobe Primetime supporta due approcci per tradurre gli MRSS in formati supportati dagli MVPD:

* **XACML**.  Il primo approccio è in linea con lo standard OLCA.  Usa XACML, in cui i valori MRSS vengono estratti per costruire una risorsa XACMLR con attributi che si mappano agli elementi MRSS.  Questo viene poi trasmesso al MVPD.
* **REST**.  Il secondo approccio è basato su REST.  L’MRSS è codificato in base64 e trasmesso come parametro URL nella chiamata REST.

In entrambi gli approcci, l&#39;MVPD elabora la richiesta di autorizzazione includendo i valori estratti all&#39;interno del proprio flusso logico e restituendo una risposta di autorizzazione.

## Dettagli di integrazione {#integration-details}

* Risorsa strutturata XACML basata su OLCA
* Risorsa strutturata basata su REST

### Risorsa strutturata XACML basata su OLCA {#olca-based-xacml-struc-resource}

La maggior parte degli MVPD orientati ai cavi utilizza l&#39;approccio basato su XACML, ma non supporta ancora l&#39;approccio completo dei dati strutturati.  Altri MVPD che supportano XACML accettano il Titolo canale e lo accettano per l&#39;attributo ResourceID. L&#39;esempio seguente mostra l&#39;approccio completo basato su XACML. Il team di autenticazione di Adobe Primetime consiglia agli MVPD che utilizzano XACML, ma che non supportano ancora funzioni come i controlli parentali, di adattare la propria integrazione XACML al seguente esempio:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability
```

### Risorsa strutturata basata su REST {#rest-based-struct-resource}

Alcuni MVPD hanno standardizzato il seguente protocollo di autorizzazione basato su REST. Questo approccio è completo quanto l&#39;approccio XACML, ma fornisce un&#39;implementazione &quot;più leggera&quot;.

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->