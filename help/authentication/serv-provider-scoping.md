---
title: Ambito del fornitore di servizi
description: Ambito del fornitore di servizi
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Ambito del fornitore di servizi {#service-provoider-scoping}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

L’implementazione predefinita di un’integrazione di autenticazione Adobe Primetime con un MVPD è basata su **Specifiche OLCA**. Nella sezione Requisiti di autenticazione della specifica OLCA (6.5, identificativo dell&#39;oggetto) è indicato che è possibile indicare l&#39;ambito del provider di servizi (SP) per l&#39;identificatore dell&#39;oggetto. L&#39;identificatore dell&#39;oggetto è l&#39;ID utente offuscato che MVPD restituisce all&#39;SP.  In un’integrazione di autenticazione Adobe Primetime, è necessario che gli MVPD abilitino l’ambito delle richieste di autenticazione SP.

Con l&#39;autenticazione Adobe Primetime che assume il ruolo di SP per il programmatore, è necessario implementare una personalizzazione che abilita l&#39;ambito SP della richiesta di autenticazione.  Questo deve essere fatto in modo che l&#39;MVPD possa identificare il marchio di rete passato nell&#39;asserzione SAML al provider di identità (IdP) dell&#39;MVPD.  L’ambito può essere implementato in uno dei due modi descritti nella sezione successiva.

## Ambito del fornitore di servizi {#service-provider-scoping}

L&#39;autenticazione Adobe Primetime supporta i due modi seguenti per abilitare l&#39;ambito SP delle richieste di autenticazione:

* **L&#39;approccio dell&#39;emittente SAML.**  In questo approccio, il &quot;Requestor ID&quot; viene aggiunto alla stringa dell&#39;emittente SAML nella richiesta di autenticazione SAML.

* **Approccio della proprietà di ambito personalizzato.**  In questo approccio, il &quot;Requestor ID&quot; è incluso esplicitamente come proprietà personalizzata &quot;Scoping&quot; nella richiesta di autenticazione SAML.

>[!NOTE]
>
>Il &quot;Requestor ID&quot; è il modo in cui l’autenticazione Adobe Primetime si riferisce al marchio di rete del programmatore (ad esempio: &quot;CNN&quot; è uno dei marchi della rete Turner).

### Approccio emittente SAML {#saml-issuer-approach}

Questo approccio utilizza il SAML `<Issuer>` elemento nella richiesta di autenticazione SAML, come mostrato in questo snippet:

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### Approccio a proprietà di ambito personalizzato {#custom-scoping-property-approach}

Questo approccio utilizza una proprietà personalizzata denominata &quot;Scoping&quot;, come mostrato in questo frammento di una richiesta di autenticazione SAML:

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->