---
title: Disconnessione MVPD
description: Disconnessione MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Disconnessione MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

I casi di utilizzo di disconnessione possono essere implementati tramite una richiesta di disconnessione SAML inviata all&#39;IdP o tramite la chiamata di un endpoint di disconnessione personalizzato.  Gli esempi di richieste e risposte riportati di seguito forniscono esempi dell’implementazione di disconnessione SAML.

## Esempio di richiesta di disconnessione {#sample-logout-request}

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:LogoutRequest
        Destination="https://idpcom/slo" ID="_b18de1a2-5bc2-4866-88e3-97a9cbb663ca"
        IssueInstant="2010-08-18T07:18:22.479Z"
        Reason="urn:oasis:names:tc:SAML:2.0:logout:user"
        Version="2.0"
        xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
        xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>https://saml.sp.auth.adobe.com</saml:Issuer>
    <saml:NameID
        Format="urn:oasis:names:tc:SAML:2.0:nameid format:transient">
            DkCwM54kzVs5coXH0R0IFhPSA9a
    </saml:NameID>
    <samlp:SessionIndex>L4EQmlLCIS-5hHr71z1VfOCEYWk</samlp:SessionIndex>
</samlp:LogoutRequest>
```

## Esempio di risposta di disconnessione {#sample-logout-response}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<samlp:LogoutResponse
        Destination="https://sp.auth-staging.adobe.com/sp/saml/LogoutServiceHTTPRedirectResponse"
        ID="XpsdJNdPp7PEnNxfeBubP.w4e3r"
        InResponseTo="_b18de1a2-5bc2-4866-88e3-97a9cbb663ca"
        IssueInstant="2010-08-18T07:18:24.969Z" Version="2.0"
        xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer  
        xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">https://idp.com/slo
    </saml:Issuer>
    <samlp:Status>
        <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
</samlp:LogoutResponse>
```

<!--
>[!RELATEDINFORMATION]
>* [Content Metadata Exchange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [Preflight Authorization](/help/authentication/mvpd-preflight-authz.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
-->
