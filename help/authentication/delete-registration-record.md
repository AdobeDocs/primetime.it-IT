---
title: Elimina record di registrazione
description: Elimina registro di registrazione
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Elimina record di registrazione {#delete-registration-record}

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


## Descrizione {#delete-record}

Elimina il record del codice reg e rilascia il codice reg da riutilizzare. 

| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Ad esempio:</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45RTY | App in streaming</br></br>o</br></br>Servizio programmatore | 1. ID richiedente  </br>    (componente Percorso)</br>2.  Codice di registrazione  </br>    (componente Percorso) | DELETE | Nessuno | 204 |

{style="table-layout:auto"}

</br>

| Parametro di input | Descrizione |
| --- | --- |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |
| codice di registrazione | Il valore del codice di registrazione che verrà visualizzato sul dispositivo streaming (da immettere nel flusso di autenticazione). |

{style="table-layout:auto"}

</br>

### [Torna a Riferimento API REST](/help/authentication/rest-api-reference.md)