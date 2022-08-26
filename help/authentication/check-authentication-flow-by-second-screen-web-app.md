---
title: Controlla il flusso di autenticazione in base all'app Web a seconda schermata
description: Controlla il flusso di autenticazione in base all'app Web a seconda schermata
source-git-commit: 41da00e32b83aa6ea4437f95e26598e8932c4312
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Controlla il flusso di autenticazione in base all&#39;app Web a seconda schermata {#check-authentication-flow-by-second-screen-web-app}

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

Questa API deve essere utilizzata dall&#39;app Web di accesso alla seconda schermata per confermare che l&#39;autenticazione Adobe Primetime ha riconosciuto l&#39;accesso corretto da MVPD. È consigliabile richiamare questa API prima di mostrare all’utente finale un messaggio di successo che gli istruisca di passare alla console dei dispositivi per continuare i flussi di lavoro.


| Endpoint | Chiamato  </br>Da | Ingresso   </br>Parametri | HTTP  </br>Metodo | Risposta | HTTP  </br>Risposta |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{codice di registrazione} | App Web di accesso | 1. codice di registrazione  </br>    (componente Percorso)</br>2.  richiedente  </br>    (Obbligatorio) | GET | XML o JSON contenente i dettagli dell’errore in caso di errore. | 200 - Successo   </br>403 - Vietato |

</br>

| Parametro di input | Descrizione |
| ----------------- | --------------------------------------------------------------------------------------------- |
| codice di registrazione | Valore del codice di registrazione fornito dall&#39;utente all&#39;inizio del flusso di autenticazione. |
| richiedente | Il requestorId del programmatore per il quale l&#39;operazione è valida. |


### Risposta del campione (in caso di errore) {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [Torna a Riferimento API REST](http://tve.helpdocsonline.com/rest-api-reference)
