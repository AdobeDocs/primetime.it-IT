---
title: Autorizzazione MVPD
description: Autorizzazione MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Autorizzazione MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#mvpd-authz-overview}

L’autorizzazione (AuthZ) viene eseguita tramite comunicazioni back-channel (server-to-server) tra un server back-end ospitato da un Adobe e l’endpoint MVPD AuthZ.

Per le richieste AuthZ, l’endpoint di autorizzazione deve essere in grado di elaborare almeno i seguenti parametri:

* **Uid**. ID utente ricevuto dal passaggio di autenticazione.

* **ID risorsa**. Una stringa che identifica una determinata risorsa di contenuto. Questo ID risorsa è specificato dal programmatore e l&#39;MVPD deve rafforzare le regole business su queste risorse (ad esempio, verificando che l&#39;utente sia iscritto a un determinato canale).

Oltre a determinare se l’utente è autorizzato, la risposta deve includere il time-to-live (TTL) della presente autorizzazione, ossia quando l’autorizzazione scade. Se il TTL non è impostato, la richiesta AuthZ avrà esito negativo.  Per questo motivo, **il TTL è un’impostazione di configurazione obbligatoria sul lato dell’autenticazione di Adobe Primetime**, al fine di coprire il caso in cui un MVPD non include il TTL nella loro richiesta.

## Richiesta di autorizzazione {#authz-req}

Una richiesta AuthZ deve includere un oggetto per conto del quale viene effettuata la richiesta, le risorse a cui l’oggetto sta tentando di accedere, l’azione che l’oggetto sta tentando di eseguire sulla risorsa e l’ambiente in cui l’operazione sta per avere luogo. Nel caso specifico dell’autenticazione Adobe Primetime, questi elementi corrispondono a:

| Elemento XACML | Corrisponde a |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Oggetto | Entità identificata dalla sessione autenticata, a cui fa riferimento l&#39;attributoValue &quot;subject-token&quot; dell&#39;asserzione SAML. |
| Risorsa | URI per la risorsa protetta. |
| Azione | VISUALIZZARE. |
| Ambiente | Include l&#39;indirizzo IP del client richiedente, come visto dall&#39;SP. |



L&#39;SP a questo punto deve preparare una XACML Authorization DecisionQuery e inviarla (tramite HTTP POST) al PDP (Policy Decision Point) per l&#39;IdP al punto di decisione dei criteri (concordato in precedenza). Di seguito è riportato un esempio di una semplice richiesta XACML (consulta le specifiche di base XACML):

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


Dopo aver ricevuto la richiesta AuthZ, il PDP dell’MVPD valuta la richiesta e determina se all’oggetto deve essere consentito di eseguire l’azione richiesta sulla risorsa. L’MVPD restituisce quindi una risposta con una decisione, un codice di stato e un messaggio, come descritto in Risposta all’autorizzazione di seguito.

## Risposta all’autorizzazione {#authz-response}

La risposta alla richiesta AuthZ viene dopo che l&#39;MVPD valuta la richiesta e applica le regole aziendali richieste per determinare se l&#39;oggetto è autorizzato a eseguire l&#39;azione richiesta sulla risorsa . La risposta restituita all&#39;autenticazione Adobe Primetime viene nuovamente espressa seguendo la specifica di base XACML con una decisione, un codice di stato, un messaggio e obblighi che l&#39;SP ha come punto di applicazione dei criteri (PEP). Esempio di risposta :

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

Di seguito è riportato un elenco degli obblighi DENY che l’autenticazione Adobe Primetime supporta e consente ai programmatori di soddisfare:

* **abbandono:tve:xacml:2.0:obligations:limit-pc** - Il Sottoscrittore non ha effettuato un controllo parentale e l&#39;SP deve adottare le misure appropriate per limitare l&#39;accesso a questo contenuto.

* **abbandono:tve:xacml:2.0:obligations:aggiornamento** - Il Sottoscrittore non dispone di un livello di abbonamento adeguato.  Per accedere al contenuto è necessario aggiornare la sottoscrizione.

L’autenticazione Adobe Primetime supporta i seguenti **PERMESSO** Obblighi e possibilità per i programmatori di adempiere:

* **abbandono:cablelabs:olca:1.0:obligations:log** - Adobe Pass registra la transazione e può rendere disponibile tramite il meccanismo di reporting concordato.

* **abbandono:cablelabs:olca:1.0:obligations:re-authz** - L’autenticazione Adobe Primetime aggiorna l’autorizzazione nuovamente in n secondi (specificato come argomento dell’obbligo tramite un attributo XACML Assignment - vedi le specifiche di base XACML , sezione 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->