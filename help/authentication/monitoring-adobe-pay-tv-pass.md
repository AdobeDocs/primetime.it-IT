---
title: Monitoraggio dell’autenticazione Adobe Primetime
description: Monitoraggio dell’autenticazione Adobe Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Monitoraggio dell’autenticazione Adobe Primetime {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro}

I clienti possono utilizzare [Nagios](http://www.nagios.org) o altri strumenti per verificare se l’autenticazione Adobe Primetime è attiva o disattivata. 

## Monitoraggio degli endpoint {#monitoring-endpoints}

### Endpoint che è possibile monitorare {#endpoints-to-monitor}

* Endpoint di configurazione per tutte le piattaforme: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`- È disponibile tramite HTTP o HTTPS (a seconda della scelta effettuata dallo sviluppatore del provider di contenuti). Se manca questo endpoint, il contenuto non sarà disponibile su tutte le piattaforme e tutti gli MVPD. Per l’API REST senza client abbiamo anche il seguente endpoint:  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* I seguenti endpoint fanno parte dell’SDK web per l’autenticazione Adobe Primetime.  Se manca significa che pay-TVpass è giù per tutti i programmatori e tutte le proprietà web:

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### Endpoint da non monitorare {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

   Si otterrà sempre un errore 503, perché questo endpoint necessita di una risposta SAML MVPD su di esso.

* Altri endpoint di diritto - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

Non è possibile monitorare questi endpoint perché richiedono un payload per una risposta pertinente.
