---
title: Integrazione SAML MVPD proxy
description: Integrazione SAML MVPD proxy
exl-id: 6c83e703-d8cd-476b-8514-05b8230902be
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# Integrazione SAML MVPD proxy

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview-proxy-mvpd-saml-int}

Questo documento descrive il flusso di autenticazione SAML per le integrazioni Proxy.  Questi flussi dipendono dai dati di configurazione proxy presenti nella configurazione del server di autenticazione di Adobe Primetime. Il Proxy MVPD invia i dati di configurazione proxy al server di autenticazione Adobe Primetime tramite il Proxy Web Service di autenticazione Adobe Primetime.

## Dati configurazione proxy {#proxy-config-data}

Ogni proxy MVPD fornisce i dati di configurazione proxy per i propri MVPD proxy al servizio Web proxy di autenticazione di Adobe Primetime.  Dettagli relativi a che sono descritti nella documentazione del servizio web proxy.   Affinché il flusso AuthN SAML funzioni, i dati di configurazione proxy devono includere le seguenti proprietà:

| Proprietà | Descrizione |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID MVPD | Stringa che rappresenta internamente il file MVPD proxy per l’autenticazione Adobe Primetime.  Da confermare con Adobe come univoco nel contesto dell’autenticazione di Adobe Primetime. |
| URL logo predefinito MVPD | URL a un logo che può essere visualizzato dall&#39;utente in un&#39;esperienza di selezione MVPD.  Utilizza uno sfondo trasparente. |
| Nome visualizzato MVPD | Stringa da utilizzare come testo del nome visualizzato che potrebbe essere visualizzato con il logo, potenzialmente come testo alternativo. |



## Flussi di integrazione SAML {#saml-int-flows}

Quando un abbonato MVPD visita il sito o l’applicazione di un programmatore, l’autenticazione Adobe Primetime risponde a una chiamata API dal sito o dall’applicazione con un elenco di MVPD attivati per quel programmatore.  L&#39;integrazione può essere diretta o proxy; non c&#39;è distinzione tra di loro per il programmatore. Questo consente ai programmatori di presentare l&#39;elenco degli MVPD attivi in qualsiasi modo lo ritengano opportuno. L&#39;utente che effettua l&#39;abbonamento sceglie il proprio MVPD e l&#39;autenticazione Adobe Primetime reindirizza l&#39;utente al provider di identità specifico dell&#39;MVPD.

Nel caso di un proxy MVPD integrato, l&#39;integrazione viene eseguita tra l&#39;autenticazione di Adobe Primetime e il proxy MVPD. L’autenticazione di Adobe Primetime invia la richiesta di autenticazione dell’utente al proxy MVPD, che a sua volta gestisce il reindirizzamento. Affinché il proxy MVPD sappia dove reindirizzare la richiesta di autenticazione dell&#39;utente, l&#39;autenticazione Adobe Primetime invia un identificatore MVPD nella richiesta di autenticazione SAML.  Questo identificatore è l&#39;ID MVPD specificato dal provider proxy tramite il servizio Web proxy come specificato in precedenza.

### Autenticazione {#authn-saml-int}

Per integrare l’autenticazione Adobe Primetime con un MVPD proxy è necessario quanto segue:

* Un MVPD proxy ha fornito un elenco di MVPD proxy inviati al servizio Web proxy Adobe

* Metadati SAML per il proxy MVPD padre

* (Consigliato) - Il MVPD proxy gestisce il reindirizzamento aggiuntivo all&#39;URL della pagina di accesso del MVPD proxy

* Il proxy MVPD deve aprire le porte 443 e 80 per i seguenti IP:
   * 192.150.4.5
   * 192.150.10.200
   * 192.150.11.4
   * 4.53.93.130
   * 193.105.140.131
   * 193.105.140.132
   * 76.74.170.204
   * 63.140.39.4
   * 66.235.132.38
   * 66.235.139.38
   * 66.235.139.168


#### Richiesta e risposta SAML di autenticazione {#authn-saml-req-resp}

Nella richiesta AuthN SAML, le integrazioni proxy includono la seguente proprietà aggiuntiva che deve essere gestita dal proxy MVPD.  Questa proprietà è necessaria per elaborare correttamente il richiedente per conto dell’MVPD proxy e per eseguire il rendering dell’esperienza di accesso corretta. Questa proprietà è evidenziata nella richiesta di esempio seguente.

**Scoping, proprietà** - Include un elemento IDPEntry che include il valore MVPD_ID e il nome MVPD specifici.  Rappresenta l&#39;MVPD che l&#39;utente ha effettivamente selezionato dal selettore del programmatore e corrisponde all&#39;MVPD_ID specificato nel servizio Web proxy.

Esiste un’ulteriore proprietà di ambito per RequestorID che può essere utilizzata per personalizzare l’accesso a un particolare brand del programmatore (se necessario). Oppure, può essere utilizzato semplicemente per le analisi da cui proviene la richiesta.

Nella risposta AuthN SAML, il Proxy MVPD deve specificare il Proxy MVPD come Entità IdP nelle seguenti proprietà:

* Emittente SAML
* Qualificatore nome


**Esempio di richiesta AuthN**

```XML
<samlp:AuthnRequest
  AssertionConsumerServiceURL="https://sp.auth-staging.adobe.com/sp/saml/SAMLAssertionConsumer"
  Destination="DESTIONATION_URL"
  ForceAuthn="false"
  ID="_4cb70308-b445-462e-b044-f7d0323dde0c"
  IsPassive="false"
  IssueInstant="2012-04-03T15:41:25.884Z"
  ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
  Version="2.0"
  xmlns:ds="http://www.w3.org/2000/09/xmldsig#"
  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
      https://saml.sp.auth-staging.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
        ...........
    </ds:Signature>
    <samlp:NameIDPolicy AllowCreate="true"
                        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                        SPNameQualifier="https://saml.sp.auth-staging.adobe.com"
                        xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" />
    <samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
        <samlp:IDPList xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
            <samlp:IDPEntry Name="MVPD NAME" ProviderID="MVPD_ID"/>
        </samlp:IDPList>
        <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
          RequestorID-Value
        </samlp:RequesterID>
    </samlp:Scoping>
</samlp:AuthnRequest>
```


**Esempio di risposta AuthN**

```XML
<samlp:Response Destination="https://sp.auth-staging.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_1d39be60-66de-012f-bfd5-0030488a31a4"
                InResponseTo="_4cb70308-b445-462e-b044-f7d0323dde0c"
                IssueInstant="2012-04-12T15:00:06Z"
                Version="2.0"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" >
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">ISSUER_VALUE</saml:Issuer>
    <samlp:Status>
        <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="_1d39c280-66de-012f-bfd6-0030488a31a4"
                    IssueInstant="2012-04-12T15:00:06Z"
                    Version="2.0"
                    xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" >
        <saml:Issuer>ISSUER_VALUE</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            ...........
        </ds:Signature>
        <saml:Subject>
            <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                         NameQualifier="IDP_NameQualifier"
                         SPNameQualifier="https://saml.sp.auth-staging.adobe.com">
                oRD6ALr5jlzkofNR1OaSCDbC6GaXV1cq8gF7Eotf
            </saml:NameID>
            <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
                <saml:SubjectConfirmationData
                  InResponseTo="_4cb70308-b445-462e-b044-f7d0323dde0c"
                  NotOnOrAfter="2012-04-12T15:10:06Z"
                  Recipient="https://sp.auth-staging.adobe.com/sp/saml/SAMLAssertionConsumer" />
            </saml:SubjectConfirmation>
        </saml:Subject>
        <saml:Conditions NotBefore="2012-04-12T15:00:06Z"
                         NotOnOrAfter="2012-04-12T15:10:06Z">
            <saml:AudienceRestriction>
                <saml:Audience>https://saml.sp.auth-staging.adobe.com</saml:Audience>
            </saml:AudienceRestriction>
        </saml:Conditions>
        <saml:AuthnStatement AuthnInstant="2012-04-12T15:00:06Z"
                             SessionIndex="f6d15540cf27966115028d35c94eefb9" >
            <saml:AuthnContext>
                <saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
                </saml:AuthnContextClassRef>
            </saml:AuthnContext>
        </saml:AuthnStatement>
    </saml:Assertion>
</samlp:Response>
```

### Autorizzazione {#authz-proxy-mvpd-saml-int}

Per la parte relativa all&#39;autorizzazione, l&#39;MVPD dovrebbe accettare per l&#39;autorizzazione la risorsa specificata dal programmatore.  Nella maggior parte dei casi, si tratta di un identificatore stringa per la rete del canale, ad esempio TBS o TNT.

#### Richiesta e risposta SAML di autorizzazione {#authz-saml-req-resp}

Nella risposta AuthZ, l&#39;AUTORITÀ DI CERTIFICAZIONE deve corrispondere all&#39;AUTORITÀ DI CERTIFICAZIONE dalla risposta SAML, che deve essere l&#39;identificatore MVPD proxy.

**Esempio di richiesta XACML AuthZ**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/">
<soap11:Header/>
<soap11:Body>
    <xacml-samlp:XACMLAuthzDecisionQuery
            xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
            ID="_c2346a8f2c9cfb205b6b8bf12c2db4d0" IssueInstant="2012-04-12T15:07:51.280Z" Version="2.0">
        <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com
        </saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
                <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
                <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
                <ds:Reference URI="#_c2346a8f2c9cfb205b6b8bf12c2db4d0">
                    <ds:Transforms>
                        <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
                        <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#">
                            <ec:InclusiveNamespaces xmlns:ec="http://www.w3.org/2001/10/xml-exc-c14n#"
                                                    PrefixList="ds saml xacml-context xacml-samlp"/>
                        </ds:Transform>
                    </ds:Transforms>
                    <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
                    <ds:DigestValue>GmEkSZI+SDS1i4vV2ApGh0mx1X4=</ds:DigestValue>
                </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>..........</ds:SignatureValue>
        </ds:Signature>
        <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">          
            <xacml-context:Subject
              SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject">
                <xacml-context:Attribute
                  AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id"
                  DataType="http://www.w3.org/2001/XMLSchema#string">
                    <xacml-context:AttributeValue
                      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                      xsi:type="xacml-context:AttributeValueType">
                        oRD6ALr5jlzkofNR1OaSCDbC6GaXV1cq8gF7Eotf
                    </xacml-context:AttributeValue>
                </xacml-context:Attribute>
            </xacml-context:Subject>
            <xacml-context:Resource>
                <xacml-context:Attribute
                  AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
                  DataType="http://www.w3.org/2001/XMLSchema#string">
                    <xacml-context:AttributeValue
                      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                      xsi:type="xacml-context:AttributeValueType">TBS
                    </xacml-context:AttributeValue>
                </xacml-context:Attribute>
            </xacml-context:Resource>
            <xacml-context:Action>
                <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
                                         DataType="http://www.w3.org/2001/XMLSchema#string">
                    <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                                  xsi:type="xacml-context:AttributeValueType">VIEW
                    </xacml-context:AttributeValue>
                </xacml-context:Attribute>
            </xacml-context:Action>
            <xacml-context:Environment>
                <xacml-context:Attribute
                  AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
                  DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress">
                    <xacml-context:AttributeValue
                      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                      xsi:type="xacml-context:AttributeValueType">127.0.0.1
                    </xacml-context:AttributeValue>
                </xacml-context:Attribute>
            </xacml-context:Environment>
        </xacml-context:Request>
    </xacml-samlp:XACMLAuthzDecisionQuery>
</soap11:Body>
</soap11:Envelope>
```

**Esempio di risposta XACML AuthZ (autorizzazione concessa)**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap-env:Envelope xmlns:soap-env="http://schemas.xmlsoap.org/soap/envelope/">
    <soap-env:Body>
        <samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="_311fa030-66df-012f-bfd7-0030488a31a4"
                        IssueInstant="2012-04-12T15:07:49Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">ISSUER</saml:Issuer>
            <samlp:Status>
                <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
            </samlp:Status>
            <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
                <ds:SignedInfo>
                    <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
                    <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
                    <ds:Reference URI="#_311fa030-66df-012f-bfd7-0030488a31a4">
                        <ds:Transforms>
                            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
                            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
                        </ds:Transforms>
                        <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
                        <ds:DigestValue>2+fDBPYnOT1w5dufJZoVsgckRkM=</ds:DigestValue>
                    </ds:Reference>
                </ds:SignedInfo>
                <ds:SignatureValue>..........</ds:SignatureValue>
                <ds:KeyInfo>
                    <ds:X509Data>
                        <ds:X509Certificate>.........</ds:X509Certificate>
                    </ds:X509Data>
                </ds:KeyInfo>
            </ds:Signature>
            <xacml-samlp:Assertion xmlns:xacml-samlp="urn:oasis:names:tc:SAML:2.0:assertion"
                                   ID="_311fa5a0-66df-012f-bfd8-0030488a31a4" IssueInstant="2012-04-12T15:07:49Z"
                                   Version="2.0">
                <xacml-samlp:Issuer>ISSUER</xacml-samlp:Issuer>
                <xacml-samlp:Conditions NotBefore="2012-04-12T15:07:49Z" NotOnOrAfter="2012-04-13T15:07:49Z">
                    <xacml-samlp:AudienceRestriction>
                        <xacml-samlp:Audience>https://saml.sp.auth-staging.adobe.com</xacml-samlp:Audience>
                    </xacml-samlp:AudienceRestriction>
                </xacml-samlp:Conditions>
                <xacml-saml:XACMLAuthzDecisionStatement
                        xmlns:xacml-saml="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:assertion"
                        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                    <xacml-context:Response xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                        <xacml-context:Result ResourceId="TBS">
                            <xacml-context:Decision>Permit</xacml-context:Decision>
                        </xacml-context:Result>
                    </xacml-context:Response>
                </xacml-saml:XACMLAuthzDecisionStatement>
            </xacml-samlp:Assertion>
        </samlp:Response>
    </soap-env:Body>
</soap-env:Envelope>
```

**Esempio di risposta XACML AuthZ (autorizzazione negata)**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap-env:Envelope xmlns:soap-env="http://schemas.xmlsoap.org/soap/envelope/">
<soap-env:Body>
    <samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="_69ed8d80-66df-012f-bfda-0030488a31a4"
                    IssueInstant="2012-04-12T15:09:24Z" Version="2.0">
        <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">ISSUER</saml:Issuer>
        <samlp:Status>
            <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
        </samlp:Status>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
                <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
                <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
                <ds:Reference URI="#_69ed8d80-66df-012f-bfda-0030488a31a4">
                    <ds:Transforms>
                        <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
                        <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
                    </ds:Transforms>
                    <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
                    <ds:DigestValue>2SXNFA4pb/283wq5FVQdp4Ms5SQ=</ds:DigestValue>
                </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>........</ds:SignatureValue>
            <ds:KeyInfo>
                <ds:X509Data>
                    <ds:X509Certificate>........</ds:X509Certificate>
                </ds:X509Data>
            </ds:KeyInfo>
        </ds:Signature>
        <xacml-samlp:Assertion xmlns:xacml-samlp="urn:oasis:names:tc:SAML:2.0:assertion"
                               ID="_69ed91e0-66df-012f-bfdb-0030488a31a4" IssueInstant="2012-04-12T15:09:24Z"
                               Version="2.0">
            <xacml-samlp:Issuer>ISSUER</xacml-samlp:Issuer>
            <xacml-samlp:Conditions NotBefore="2012-04-12T15:09:24Z" NotOnOrAfter="2012-04-13T15:09:24Z">
                <xacml-samlp:AudienceRestriction>
                    <xacml-samlp:Audience>https://saml.sp.auth-staging.adobe.com</xacml-samlp:Audience>
                </xacml-samlp:AudienceRestriction>
            </xacml-samlp:Conditions>
            <xacml-saml:XACMLAuthzDecisionStatement
                    xmlns:xacml-saml="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:assertion"
                    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                <xacml-context:Response xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                    <xacml-context:Result ResourceId="NOT_Authorized_Resouce">
                        <xacml-context:Decision>Deny</xacml-context:Decision>
                    </xacml-context:Result>
                </xacml-context:Response>
            </xacml-saml:XACMLAuthzDecisionStatement>
        </xacml-samlp:Assertion>
    </samlp:Response>
</soap-env:Body>
</soap-env:Envelope>
```

<!--
>![RelatedInformation]
>* [ProxyMVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Service Provider Scoping](/help/authentication/serv-provider-scoping.md)
-->
