---
title: Vantaggi dell’utilizzo del parametro client deviceType nelle metriche di autenticazione Primetime
description: Vantaggi dell’utilizzo del parametro client deviceType nelle metriche di autenticazione Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Vantaggi dell’utilizzo del parametro client deviceType nelle metriche di autenticazione Primetime {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Contesto

Anche se opzionale, il parametro `deviceType` dall’API senza client, se presente, viene utilizzato nelle metriche di autenticazione di Primetime che vengono esposte tramite [Monitoraggio del servizio di adesione](/help/authentication/entitlement-service-monitoring-overview.md).

Considerando che la connessione tra `deviceType` e il relativo **vantaggi** in base alle metriche di autenticazione di Primetime non è stato inizialmente dichiarato, l&#39;ambito di questa nota tecnica è quello di aggiungere ulteriori informazioni su di esse.

## Spiegazione

La `deviceType` era presente nell’API Clientless dalla prima versione, ma le sue implicazioni sulle metriche di autenticazione Primetime sono state aggiunte in una versione più recente.



>[!IMPORTANT]
>
>Se il parametro `deviceType` è impostato correttamente e ha le seguenti caratteristiche **beneficio** nel monitoraggio del servizio di abilitazione: offre metriche che [suddivisi per tipo di dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) quando utilizzi Clientless, in modo che sia possibile eseguire diversi tipi di analisi per esempio Roku, AppleTV, Xbox ecc.


Per ulteriori informazioni sull’API di monitoraggio del servizio di adesione, consulta [albero di espansione,](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) che illustra [dimensioni](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) (risorse) disponibili in ESM 2.0.

>[!NOTE]
>
>Il contenuto di questa nota tecnica è stato aggiunto anche al [API senza client](#clientless_device_type).




## Implementazione

Per sfruttare appieno le metriche di autenticazione di Primetime, sono disponibili 2 tipi di [API senza client](#web_srvs_summary) che sono attualmente in uso e che devono avere `deviceType` set:

1. API che hanno `regcode` come parametro richiesto e utilizzerà il `deviceType` che è stato impostato durante la creazione del `regcode`, con la seguente chiamata API:
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. API che hanno `deviceType` come parametro opzionale:
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/autorizzare](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/token/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/token/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preautorizzare](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

Si consiglia di utilizzare il `deviceType` e passa il tipo di dispositivo Clientless corretto per tutte le API.


