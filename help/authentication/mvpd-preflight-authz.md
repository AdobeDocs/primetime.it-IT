---
title: Autorizzazione di verifica preliminare MVPD
description: Autorizzazione di verifica preliminare MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---


# Autorizzazione di verifica preliminare MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#mvpd-preflight-authz-intro}

&quot;Autorizzazione Preflight&quot; è un controllo di autorizzazione leggero per più risorse. I programmatori lo utilizzano principalmente per decorare le loro interfacce utente (ad esempio, per indicare lo stato di accesso con icone di blocco e sblocco).

L’autenticazione Adobe Primetime può attualmente supportare l’autorizzazione di verifica preliminare in due modi per gli MVPD, tramite gli attributi di risposta AuthN o tramite una richiesta AuthZ multicanale.  Gli scenari seguenti descrivono il costo/beneficio dei diversi modi in cui è possibile implementare l&#39;autorizzazione di preflight:

* **Scenario migliore** - L&#39;MVPD fornisce l&#39;elenco delle risorse preautorizzate durante la fase di autorizzazione (Multi-channel AuthZ).
* **Scenario peggiore** - Se un MVPD non supporta alcuna forma di autorizzazione per più risorse, il server di autenticazione Adobe Primetime esegue una chiamata di autorizzazione all&#39;MVPD per ogni risorsa nell&#39;elenco delle risorse. Questo scenario ha un impatto (proporzionale al numero di risorse) sul tempo di risposta per la richiesta di autorizzazione di preflight. Può aumentare il carico sia sui server Adobe che MVPD causando problemi di prestazioni. Inoltre, genererà richieste di autorizzazione / eventi di risposta senza l&#39;effettiva necessità di un gioco.
* **Obsoleto** - L&#39;MVPD fornisce l&#39;elenco delle risorse preautorizzate durante la fase di autenticazione, quindi non ci saranno chiamate di rete necessarie, nemmeno la richiesta di verifica preliminare, dal momento che l&#39;elenco è memorizzato nella cache sul client.

Sebbene gli MVPD non debbano supportare l’autorizzazione di preflight, le sezioni seguenti descrivono alcuni metodi di autorizzazione di preflight che l’autenticazione Adobe Primetime può supportare, prima di tornare allo scenario peggiore di cui sopra.

## Verifica preliminare in AuthN {#preflight-authn}

Questo scenario di verifica preliminare è compatibile con OLCA (Cableabs). La sezione 7.5.2 sulla specifica dell&#39;interfaccia di autenticazione e autorizzazione 1.0 intitolata &quot;Attribute Statement Within Authentication Assertion&quot;, descrive come una risposta di autenticazione SAML possa contenere un elenco di risorse preautorizzate. Se un IdP supporta questa funzione, il server di autenticazione Adobe Primetime sarà in grado di generare l’elenco delle risorse con priorità in fase di autenticazione e di memorizzarlo nella cache sul client insieme al token di autenticazione. Questo metodo consente inoltre di ottenere lo scenario migliore e non verranno eseguite chiamate di rete quando il programmatore chiama checkPreauthorizedResources(), dal momento che tutto è già sul client.

### Elenco risorse personalizzate nell&#39;istruzione attributo SAML {#custom-res-saml-attr}

La risposta di autenticazione SAML dell&#39;IdP include un AttributeStatement contenente i nomi delle risorse che AdobePass deve autorizzare.  Alcuni MVPD forniscono questo nel seguente formato:

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

L’esempio di cui sopra presenta un elenco contenente due risorse preautorizzate: &quot;MMOD&quot; e &quot;Olympic2012&quot;.

In questo modo si ottiene effettivamente lo scenario migliore e non verranno eseguite chiamate di rete quando il programmatore chiama checkPreauthorizedResources(), poiché tutto è già sul client.

## Verifica preliminare multicanale in AuthZ {#preflight-multich-authz}

Questa implementazione di verifica preliminare è anche compatibile con OLCA (Cablelabs).  La specifica 1.0 dell&#39;interfaccia di autenticazione e autorizzazione (sezioni 7.5.3 e 7.5.4) descrive i metodi per richiedere informazioni sull&#39;autorizzazione da un MVPD utilizzando le asserzioni SAML o XACML. Questo è il modo consigliato per eseguire query sullo stato di autorizzazione per gli MVPD che non lo supportano come parte del flusso di autenticazione. L’autenticazione Adobe Primetime genera una singola chiamata di rete all’MVPD per recuperare l’elenco delle risorse autorizzate.


L’autenticazione Adobe Primetime riceve l’elenco delle risorse dall’applicazione del programmatore. L’integrazione MVPD di Adobe Primetime Authentication può quindi effettuare una chiamata AuthZ che include tutte le risorse, quindi analizzare la risposta ed estrarre le decisioni di autorizzazione/negazione multiple.  Il flusso per la verifica preliminare con lo scenario AuthZ multicanale funziona come segue:

1. L’app del programmatore invia un elenco di risorse separato da virgole tramite l’API del client di preflight, ad esempio: &quot;TestChannel1,TestChannel2,TestChannel3&quot;.
1. La chiamata di richiesta di verifica preliminare MVPD AuthZ contiene le risorse multiple e presenta la seguente struttura:

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## Autorizzazione Personalizzata Per Più Risorse {#custom-authz}

Alcuni MVPD dispongono di endpoint di autorizzazione che supportano l&#39;autorizzazione per più risorse in una richiesta, ma non rientrano nello scenario descritto in Multi-channel AuthZ. Questi MVPD specifici richiedono un lavoro personalizzato.

Adobe può anche supportare più autorizzazioni per i canali senza apportare modifiche all&#39;implementazione esistente.  Questo approccio deve essere rivisto tra l&#39;Adobe e il team tecnico MVPD per garantire che funzioni come previsto.

## MVPD che supportano l&#39;autorizzazione di preflight {#mvpds-supp-preflight-authz}

Nella tabella seguente sono elencati gli MVPD che supportano l’autorizzazione di verifica preliminare, insieme al tipo di verifica preliminare supportato e alle limitazioni note:

| Approccio di verifica preliminare | MVPD | Note |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| AuthZ multicanale | Comcast AT&amp;T Proxy Clearleap Charter_Direct Proxy GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |  |
| Line-up dei canali nei metadati utente | Collegamento improvviso HTC | Anche tutte le integrazioni dirette di Synacor supportano questo approccio. |
| Fork e join | Tutti gli altri non elencati sopra | Il numero massimo predefinito di risorse controllate = 5. |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
