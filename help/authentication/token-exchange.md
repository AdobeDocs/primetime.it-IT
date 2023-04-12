---
title: Scambiare un token SSO di Platform per un token di Adobe
description: Scambiare un token SSO di Platform per un token di Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# Scambiare un token SSO di Platform per un token di Adobe {#exchange-a-platform-sso-token-for-an-adobe-token}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Endpoint API REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produzione - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descrizione {#description}

Consente lo &quot;scambio&quot; di un profilo SSO di Platform per un token di Adobe.

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/token/autenticazione | App in streaming</br></br>o</br></br>Servizio programmatore | 1. richiedente (obbligatorio)</br>    </br>2.  deviceId (obbligatorio)</br>    </br>3.  mvpd (obbligatorio)</br>    </br>4.  deviceType (obbligatorio)</br>    </br>5.  SAMLResponse (obbligatorio)</br>    </br>6.  deviceUser (obsoleto)</br>    </br>7.  appId (obsoleto) | POST | La risposta corretta sarà No Content (Nessun contenuto) 204, il che indica che il token è stato creato correttamente ed è pronto per l’uso per i flussi di autenticazione. | 204 - Nessun contenuto   </br>400 - Richiesta errata |


| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| deviceId | Byte dell&#39;ID dispositivo. |
| mvpd | ID MVPD per il quale l&#39;operazione è valida. |
| deviceType | Piattaforma Apple per la quale stiamo tentando di ottenere una richiesta di profilo.  O **iOS** o **tvOS**. |
| SAMLResponse | Il profilo effettivo restituito da Platform SSO. |
| _deviceUser_ | Identificatore utente del dispositivo. |
| _appId_ | ID/nome dell&#39;applicazione. |


