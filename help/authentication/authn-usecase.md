---
title: Autenticazione MVPD
description: Autenticazione MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# Autenticazione MVPD {#mvpd-authn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#mvpd-authn-overview}

Il ruolo effettivo del provider di servizi (SP) è detenuto da un programmatore, ma l&#39;autenticazione Adobe Primetime funge da proxy SP per quel programmatore. L’utilizzo dell’autenticazione Adobe Primetime come intermediario consente sia agli MVPD che ai programmatori di evitare di dover personalizzare i processi di adesione caso per caso.

I passaggi seguenti presentano la sequenza di eventi, utilizzando l&#39;autenticazione Adobe Primetime, quando un programmatore richiede l&#39;autenticazione da un MVPD che supporta SAML. Il componente di Adobe Primetime Authentication Access Enabler è attivo sul client dell&#39;utente/utente che ha effettuato l&#39;abbonamento. Da lì, Access Enabler facilita tutti i passaggi del flusso di autenticazione.

1. Quando l&#39;utente richiede l&#39;accesso al contenuto protetto, Access Enabler avvia l&#39;autenticazione (AuthN) per conto del programmatore (SP).
1. L&#39;app dell&#39;SP presenta all&#39;utente un &quot;MVPD Picker&quot; per ottenere il proprio provider di Pay TV (MVPD). L&#39;SP reindirizza quindi il browser dell&#39;utente al servizio del provider di identità (IdP) dell&#39;MVPD selezionato.  Questo è &quot;**Accesso avviato dal programmatore**&quot;.  L&#39;MVPD invia la risposta dell&#39;IdP al servizio consumer di asserzione SAML di Adobe, dove viene elaborato.
1. Infine, Access Enabler reindirizza il browser al sito SP, informando l&#39;SP dello stato (riuscito/guasto) della richiesta AuthN.

## Richiesta di autenticazione {#authn-req}

Come illustrato nei passaggi precedenti, durante il flusso AuthN un MVPD deve accettare una richiesta AuthN basata su SAML e inviare una risposta SAML AuthN.

La [Specifiche dell&#39;interfaccia di autenticazione e autorizzazione per l&#39;accesso ai contenuti online (OLCA)](https://www.cablelabs.com/specifications/search?query=&amp;category=&amp;subcat=&amp;doctype=&amp;content=false&amp;archives=false){target=_blanck} presenta una richiesta e una risposta standard di AuthN. Sebbene l’autenticazione Adobe Primetime non richieda agli MVPD di basare i messaggi di adesione su questo standard, l’analisi delle specifiche può fornire informazioni sugli attributi chiave richiesti per una transazione AuthN.

>[!NOTE]
>
>La richiesta AuthN che un MVPD riceve con l’autenticazione Adobe Primetime contiene una firma digitale. Tuttavia, l’esempio seguente non mostra una firma, per motivi di brevità. Per un esempio che mostra una firma digitale, vedere l’esempio in [la risposta di autenticazione](#authn-response) nelle sezioni seguenti.

Esempio di richiesta di autenticazione SAML:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest  
    AssertionConsumerServiceURL=http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer          
    Destination=http://idp.com/SSOService
    ForceAuthn="false"
    ID="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
    IsPassive="false"
    IssueInstant="2010-08-03T14:14:54.372Z"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    Version="2.0"
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
        http://saml.sp.adobe.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds=_signature_block_goes_here_
    </ds:Signature>
    <samlp:NameIDPolicy
        AllowCreate="true"
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
        SPNameQualifier="http://saml.sp.adobe.adobe.com"/>
</samlp:AuthnRequest> 
```

La tabella seguente spiega gli attributi e i tag che devono trovarsi in una richiesta di autenticazione, con i valori previsti predefiniti.

**Dettagli della richiesta di autenticazione SAML**

| samlp:AuthnRequest | &lt;authnrequest> rilasciato dal fornitore di servizi al provider di identità. |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AssertionConsumerServiceURL | Questo è l&#39;endpoint di Adobe da utilizzare nella risposta successiva. Valore predefinito: **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer** |
| Destinazione | Un riferimento URI che indica l’indirizzo a cui è stata inviata la richiesta. Ciò è utile per impedire l’inoltro dannoso delle richieste a destinatari non intenzionali, una protezione richiesta da alcuni binding dei protocolli. Se è presente, il destinatario effettivo DEVE verificare che il riferimento URI identifichi la posizione in cui è stato ricevuto il messaggio. In caso contrario, la richiesta DEVE essere scartata. Alcuni binding del protocollo possono richiedere l’utilizzo di questo attributo. |
| ForceAuthn | L&#39;attributo ForceAuthn, se presente con un valore true, obbliga il provider di identità a stabilire di recente questa identità, invece di affidarsi a una sessione esistente che può avere con l&#39;entità principale. |
| ID | Identificatore per la richiesta. Vedi [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} sezione 1.3.4 per maggiori dettagli. |
| IsPassive | Un valore booleano. Se &quot;true&quot;, il provider di identità e l&#39;agente utente stesso NON DEVONO prendere visibilmente il controllo dell&#39;interfaccia utente dal richiedente e interagire con il presentatore in modo visibile. Se non viene fornito un valore, il valore predefinito è &quot;false&quot;. |
| IssueInstant | L&#39;istante di emissione della risposta. Il valore dell’ora viene codificato in UTC come descritto in [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} Sezione 1.3.3. |
| ProtocolBinding | Un riferimento URI che identifica un binding del protocollo SAML da utilizzare per restituire &lt;response> messaggio. Vedi [SAMLBind] per ulteriori informazioni sui binding dei protocolli e sui riferimenti URI definiti per tali riferimenti. Valore predefinito : abbandono:oasis:nomi:tc:SAML:2.0:bindings:HTTP-POST |
| Versione | Versione della richiesta. |
| saml:Issuer | Identifica l’entità che ha generato il messaggio di risposta. (Per ulteriori informazioni su questo elemento, vedi la sezione 2.2.5 di SAML core 2.0-os |
| ds:Signature | Una firma XML che protegge l&#39;integrità dell&#39;emittente dell&#39;asserzione e la autentica, come descritto nella sezione 5 di SAML core 2.0-os |
| samlp:NameIDPolicy | Specifica i vincoli relativi all&#39;identificatore del nome da utilizzare per rappresentare l&#39;oggetto richiesto. |
| AllowCreate | Valore booleano utilizzato per indicare se al provider di identità è consentito, nel corso del soddisfacimento della richiesta, creare un nuovo identificativo per rappresentare l&#39;entità. Predefinito: true |
| Formato | Specifica il riferimento URI corrispondente al formato di identificatore del nome Predefinito: abbandono:oasis:nomi:tc:SAML:2.0:nameid-format:un Adobe transitorio consiglia: abbandono:oasis:nomi:tc:SAML:2.0:nameid-format:persistente |
| SPNameQualifier | Facoltativamente, specifica che l&#39;identificatore dell&#39;oggetto asserzione deve essere restituito (o creato) nello spazio dei nomi di un provider di servizi diverso dal richiedente. Predefinito : http://saml.sp.adobe.adobe.com |

## Risposta di autenticazione {#authn-response}

Dopo aver ricevuto e gestito la richiesta di autenticazione, l&#39;MVPD deve ora inviare una risposta di autenticazione.

**Risposta di autenticazione SAML di esempio**

```XML
<?xml version="1.0" encoding="UTF-8"?> 
<samlp:Response Destination="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_0ac3a9dd5dae0ce05de20912af6f4f83a00ce19587"                             
                InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                IssueInstant="2010-08-17T11:17:50Z" Version="2.0"              
                xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
             http://idp.com/SSOService
    </saml:Issuer>
    <samlp:Status>
       <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="pfxb0662d76-17a2-a7bd-375f-c11046a86742"
                   IssueInstant="2010-08-17T11:17:50Z"
                   Version="2.0">
        <saml:Issuer>http://idp.com/SSOService</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
          <ds:SignedInfo>
            <ds:CanonicalizationMethod
                     Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
            <ds:SignatureMethod
                     Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
            <ds:Reference URI="#pfxb0662d76-17a2-a7bd-375f-c11046a86742">
              <ds:Transforms>
                 <ds:Transform
                    Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>        
                 <ds:Transform
                            Algorithm=http://www.w3.org/2001/10/xml-exc-c14n#"/>
              </ds:Transforms>
              <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
              <ds:DigestValue>LgaPI2ASx/fHsoq0rB15Zk+CRQ0=</ds:DigestValue>
            </ds:Reference>
          </ds:SignedInfo>
          <ds:SignatureValue>
                POw/mCKF__shortened_for_brevity__9xdktDu+iiQqmnTs/NIjV5dw==
          </ds:SignatureValue>
          <ds:KeyInfo>
            <ds:X509Data>
                <ds:X509Certificate>
                 MIIDVDCCAjygAwIBA__shortened_for_brevity_utQ==
                </ds:X509Certificate>
            </ds:X509Data>
          </ds:KeyInfo>
      </ds:Signature>
      <saml:Subject>
        <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                     SPNameQualifier="https://saml.sp.auth.adobe.com">
            _5afe9a437203354aa8480ce772acb703e6bbb8a3ad
        </saml:NameID>
        <saml:SubjectConfirmation
                     Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
            <saml:SubjectConfirmationData
                  InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                  NotOnOrAfter="2010-08-17T11:22:50Z"                                          
                  Recipient="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"/>
           </saml:SubjectConfirmation>
       </saml:Subject>
       <saml:Conditions NotBefore="2010-08-17T11:17:20Z"
                        NotOnOrAfter="2010-08-17T19:17:50Z">
           <saml:AudienceRestriction>
              <saml:Audience>https://saml.sp.auth.adobe.com</saml:Audience>
           </saml:AudienceRestriction>
       </saml:Conditions>
       <saml:AuthnStatement AuthnInstant="2010-08-17T11:17:50Z"
                   SessionIndex="_1adc7692e0fffbb1f9b944aeafce62aaa7d770cd9e">
        <saml:AuthnContext>
            <saml:AuthnContextClassRef>
                   urn:oasis:names:tc:SAML:2.0:ac:classes:Password
            </saml:AuthnContextClassRef>
        </saml:AuthnContext>
    </saml:AuthnStatement>
  </saml:Assertion>
</samlp:Response>
```


Nell’esempio precedente, l’SP di Adobe prevede di recuperare l’ID utente dall’Subject/NameId. L&#39;SP di Adobe può essere configurato per ottenere l&#39;ID utente da un attributo personalizzato definito; la risposta deve contenere un elemento come il seguente:

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**Dettagli di risposta dell&#39;autenticazione SAML**
| samlp:Risposta | Risposta ricevuta dall’autenticazione Adobe Primetime.                                                                                                                                                                                                                                                                                                                                                                                                                       | |—|—| | Destinazione | Un riferimento URI che indica l’indirizzo a cui è stata inviata la richiesta. Ciò è utile per impedire l’inoltro dannoso delle richieste a destinatari non intenzionali, una protezione richiesta da alcuni binding dei protocolli. Se è presente, il destinatario effettivo DEVE verificare che il riferimento URI identifichi la posizione in cui è stato ricevuto il messaggio. In caso contrario, la richiesta DEVE essere scartata. Alcuni binding del protocollo possono richiedere l’utilizzo di questo attributo. | | ID | Identificatore della richiesta. È di tipo xs:ID e DEVE rispettare i requisiti specificati nella sezione 1.3.4 del [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} per l’univocità dell’identificatore. I valori dell&#39;attributo ID in una richiesta e dell&#39;attributo InResponseTo nella risposta corrispondente DEVONO corrispondere.                                                                                                                                                                                         | | InResponseTo | L&#39;ID di un messaggio del protocollo SAML in risposta al quale un&#39;entità che attesta può presentare l&#39;asserzione. Il valore deve essere uguale a quello dell&#39;attributo ID inviato nella richiesta di autenticazione. Vedere SAML core 2.0-os | | IssueInstant | Momento di rilascio della richiesta.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | Versione | Versione della richiesta.                                                                                                                                                                                                                                                                                                                                                                                                                                                | | saml:Emittente | Identifica l’entità che ha generato il messaggio di richiesta. (Per ulteriori informazioni su questo elemento, vedi la sezione 2.2.5. SAML core 2.0-os ) | | samlp:Status | Codice che rappresenta lo stato della richiesta corrispondente.                                                                                                                                                                                                                                                                                                                                                                                                               | | samlp:StatusCode | Codice che rappresenta lo stato dell’attività eseguita in risposta alla richiesta corrispondente.                                                                                                                                                                                                                                                                                                                                                                       | | saml:Asserzione | Questo tipo specifica le informazioni di base comuni a tutte le asserzioni.                                                                                                                                                                                                                                                                                                                                                                                                        | | ID | Identificatore per questa asserzione.                                                                                                                                                                                                                                                                                                                                                                                                                                         | | Versione | Versione di questa asserzione.                                                                                                                                                                                                                                                                                                                                                                                                                                             | | IssueInstant | Momento di rilascio della richiesta.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | ds:Signature | Una firma XML che protegge l&#39;integrità dell&#39;emittente dell&#39;asserzione e la autentica, come descritto nella sezione 5 di SAML core 2.0-os | | ds:SignedInfo | La struttura di SignedInfo include l’algoritmo di canonicalizzazione, un algoritmo di firma e uno o più riferimenti. L&#39;elemento SignedInfo può contenere un attributo ID facoltativo che consente di farvi riferimento da altre firme e oggetti. Vedere Sintassi ed elaborazione delle firme XML | | ds:CanonicalizationMethod | CanonicalizationMethod è un elemento obbligatorio che specifica l&#39;algoritmo di canonicalizzazione applicato all&#39;elemento SignedInfo prima di eseguire i calcoli della firma. Vedere Sintassi ed elaborazione delle firme XML | | ds:SignatureMethod | SignatureMethod è un elemento obbligatorio che specifica l&#39;algoritmo utilizzato per la generazione e la convalida della firma. Questo algoritmo identifica tutte le funzioni di crittografia coinvolte nell’operazione di firma (ad esempio hashing, algoritmi di chiave pubblica, MAC, spaziatura, ecc.) Vedere Sintassi ed elaborazione delle firme XML | | ds:Reference | Il riferimento è un elemento che può verificarsi una o più volte. Specifica un algoritmo e un valore digest e, facoltativamente, un identificatore dell’oggetto da firmare, il tipo di oggetto e/o un elenco di trasformazioni da applicare prima del digestione. Vedere Sintassi ed elaborazione delle firme XML | | ds:Transforms | L’elemento Transforms facoltativo contiene un elenco ordinato di elementi Transform; descrivono come il firmatario ha ottenuto l’oggetto dati digitato. L&#39;output di ogni trasformazione funge da input per la successiva trasformazione. L&#39;input per la prima trasformazione è il risultato del riferimento all&#39;attributo URI dell&#39;elemento Reference. L&#39;output dell&#39;ultima trasformazione è l&#39;input per l&#39;algoritmo DigestMethod. Vedere Sintassi ed elaborazione delle firme XML | | ds:DigestMethod | DigestMethod è un elemento obbligatorio che identifica l&#39;algoritmo digest da applicare all&#39;oggetto firmato. Vedere Sintassi ed elaborazione delle firme XML | | ds:DigestValue | DigestValue è un elemento che contiene il valore codificato del digest. Il riassunto viene sempre codificato utilizzando base64. Vedere Sintassi ed elaborazione delle firme XML | | ds:SignatureValue | L&#39;elemento SignatureValue contiene il valore effettivo della firma digitale; viene sempre codificato utilizzando base64. Vedere Sintassi ed elaborazione delle firme XML | | ds:KeyInfo | KeyInfo è un elemento facoltativo che consente ai destinatari di ottenere la chiave necessaria per convalidare la firma. Vedere Sintassi ed elaborazione delle firme XML | | ds:X509Data | Un elemento X509Data in KeyInfo contiene uno o più identificatori di chiavi o certificati X509. Vedere Sintassi ed elaborazione delle firme XML | | ds: Certificato X509X | L’elemento X509Certificate, che contiene un codice base64 [X509v3] certificato | | saml:Subject | Oggetto della dichiarazione o delle dichiarazioni contenute nell&#39;asserzione.                                                                                                                                                                                                                                                                                                                                                                                                                          | | saml:NameID | &lt;nameid> è di tipo NameIDType (vedi la sezione 2.2.2 in SAML core 2.0-os) e viene utilizzato in vari costrutti di asserzione SAML, come &lt;subject> e &lt;subjectconfirmation> e in vari messaggi di protocollo.                                                                                                                                                                                                                                           | | Formato | Un riferimento URI che rappresenta la classificazione delle informazioni sull&#39;identificatore basato su stringhe.                                                                                                                                                                                                                                                                                                                                                                                    | | SPNameQualifier | È inoltre qualificato un nome con il nome di un fornitore di servizi o con l&#39;affiliazione di fornitori. Questo attributo fornisce un mezzo aggiuntivo per federare i nomi in base alla parte o alle parti che lo compongono.                                                                                                                                                                                                                                                                      | | saml:SubjectConfirmation | Informazioni che consentono la conferma del soggetto. Se viene fornita più di una conferma del soggetto, il soddisfacimento di una di esse è sufficiente a confermare il soggetto ai fini dell&#39;applicazione dell&#39;asserzione.                                                                                                                                                                                                                                                    | | saml:SubjectConfirmationData | Informazioni aggiuntive di conferma da utilizzare con uno specifico metodo di conferma. Ad esempio, il contenuto tipico di questo elemento potrebbe essere un <!--<ds:KeyInfo>--> come definito nella specifica Sintassi ed elaborazione firma XML | | NotOnOrAfter | Momento in cui il soggetto non può più essere confermato.                                                                                                                                                                                                                                                                                                                                                                                                            | | Destinatario | URI che specifica l’entità o la posizione in cui un’entità che attesta può presentare l’asserzione. Ad esempio, questo attributo potrebbe indicare che l&#39;asserzione deve essere consegnata a un particolare endpoint di rete al fine di impedire ad un intermediario di reindirizzarlo da un altro punto.                                                                                                                                                                                   | | saml:Condizioni | &lt;condition> funge da punto di estensione per le nuove condizioni.                                                                                                                                                                                                                                                                                                                                                                                                   | | NotBefore | L&#39;attributo NotBefore specifica l&#39;istante in cui inizia l&#39;intervallo di validità.                                                                                                                                                                                                                                                                                                                                                                                  | | saml:AudienceRestriction | &lt;audiencerestriction> specifica che l&#39;asserzione è indirizzata a uno o più tipi di pubblico specifici identificati da &lt;audience> elementi.                                                                                                                                                                                                                                                                                                                           | | saml:Audience | Un riferimento URI che identifica un pubblico previsto.                                                                                                                                                                                                                                                                                                                                                                                                                      | | saml:AuthnStatement | Un’istruzione di autenticazione.                                                                                                                                                                                                                                                                                                                                                                                                                                               | | AuthnInstant | Specifica l&#39;ora in cui si è verificata l&#39;autenticazione.                                                                                                                                                                                                                                                                                                                                                                                                                 | | SessionIndex | Specifica l&#39;indice di una sessione specifica tra l&#39;entità principale identificata dal soggetto e l&#39;autorità di autenticazione.                                                                                                                                                                                                                                                                                                                                              | | saml:AuthnContext | Contesto utilizzato dall&#39;autorità di autenticazione fino all&#39;evento di autenticazione che ha prodotto questa dichiarazione.                                                                                                                                                                                                                                                                                                                                                 | | saml:AuthnContextClassRef | Un riferimento URI che identifica una classe di contesto di autenticazione che descrive la dichiarazione di contesto di autenticazione seguente. |