---
title: Autorizzazione MVPD
description: Autorizzazione MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Autorizzazione MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#mvpd-authz-overview}

L&#39;autorizzazione (AuthZ) viene eseguita tramite comunicazioni back-channel (server-to-server) tra un server back-end ospitato da Adobe e l&#39;endpoint AuthZ MVPD.

Per le richieste AuthZ, l’endpoint di autorizzazione deve essere in grado di elaborare almeno i seguenti parametri:

* **Uid**. L’ID utente ricevuto dal passaggio di autenticazione.

* **ID risorsa**. Stringa che identifica una determinata risorsa di contenuto. Questo ID risorsa è specificato dal programmatore e l’MVPD deve rafforzare le regole di business su queste risorse (ad esempio, verificando che l’utente sia abbonato a un determinato canale).

Oltre a determinare se l’utente è autorizzato, la risposta deve includere il valore TTL (time-to-live) di questa autorizzazione, ovvero il momento in cui l’autorizzazione scade. Se il TTL non è impostato, la richiesta AuthZ avrà esito negativo.  Per questo motivo: **il TTL è un’impostazione di configurazione obbligatoria sul lato autenticazione di Adobe Primetime**, al fine di coprire il caso in cui un MVPD non includa il TTL nella sua richiesta.

## La richiesta di autorizzazione {#authz-req}

Una richiesta AuthZ deve includere un oggetto per conto del quale viene effettuata la richiesta, le risorse a cui il soggetto sta tentando di accedere, l&#39;azione che il soggetto sta tentando di eseguire sulla risorsa e l&#39;ambiente in cui l&#39;operazione sta per avere luogo. Nel caso particolare dell’autenticazione Adobe Primetime, questi elementi corrispondono a:

| Elemento XACML | Corrisponde a |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Oggetto | Principale identificato dalla sessione autenticata, a cui fa riferimento l’AttributeValue &quot;subject-token&quot; dell’asserzione SAML. |
| Risorsa | URI per la risorsa protetta. |
| Azione | VISUALIZZA. |
| Ambiente | Include l&#39;indirizzo IP del client richiedente, visualizzato dall&#39;SP. |



A questo punto, l’SP deve preparare una query di decisione di autorizzazione XACML e inviarla (tramite HTTP POST) al punto di decisione dei criteri (PDP) (precedentemente concordato) per l’IdP. Di seguito è riportato un esempio di una semplice richiesta XACML (consulta le specifiche principali XACML):

```XML
POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```


Dopo aver ricevuto la richiesta AuthZ, il PDP dell&#39;MVPD valuta la richiesta e determina se al soggetto deve essere consentito di eseguire l&#39;azione richiesta sulla risorsa. L’MVPD restituisce quindi una risposta con una decisione, un codice di stato e un messaggio, come descritto nella Risposta all’autorizzazione di seguito.

## La risposta di autorizzazione {#authz-response}

La risposta alla richiesta AuthZ viene fornita dopo che MVPD valuta la richiesta e applica le regole business richieste per determinare se al soggetto è consentito eseguire l&#39;azione richiesta sulla risorsa. La risposta restituita all’autenticazione di Adobe Primetime viene nuovamente espressa in base alle specifiche principali XACML con una decisione, un codice di stato, un messaggio e gli obblighi che l’SP ha come punto di applicazione dei criteri (PEP, Policy Enforcement Point). Di seguito è riportato un esempio di risposta:

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

Di seguito è riportato un elenco di DENY Obbligations che l’autenticazione Adobe Primetime supporta e consente ai programmatori di adempiere:

* **urn:tve:xacml:2.0:obligations:restricted-pc** - L&#39;abbonato non ha superato un controllo di protezione e l&#39;SP deve adottare misure appropriate per limitare l&#39;accesso a questo contenuto.

* **urn:tve:xacml:2.0:obligations:aggiornamento** - Il Sottoscrittore non dispone di un livello di abbonamento appropriato.  Per accedere al contenuto, è necessario aggiornare l’abbonamento.

L’autenticazione Adobe Primetime supporta quanto segue **PERMESSO** Obblighi e possibilità per i programmatori di adempierli:

* **urn:cablelabs:olca:1,0:obligations:log** : Adobe Pass registra la transazione e può renderla disponibile tramite il meccanismo di reporting concordato.

* **urn:cablelabs:olca:1,0:obligations:ri-authoring** - L’autenticazione Adobe Primetime aggiorna nuovamente l’autorizzazione in n secondi (specificati come argomento dell’obbligazione tramite un AttributeAssignment XACML - consulta le specifiche principali XACML, sezione 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->
