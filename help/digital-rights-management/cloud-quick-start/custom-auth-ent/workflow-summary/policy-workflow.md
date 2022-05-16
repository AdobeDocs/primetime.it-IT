---
title: Dettagli del flusso di lavoro dei criteri
description: Dettagli del flusso di lavoro dei criteri
copied-description: true
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Workflow API {#bees-workflow}

**Riepilogo:**

* **Criterio** - Creare un criterio DRM consapevole dell&#39;BEES che indichi che l&#39;API è necessaria per tutti i contenuti in pacchetto utilizzando questa policy.
* **Pacchetto** - Creare pacchetti di contenuti utilizzando la politica DRM consapevole delle API.
* **Autenticazione** - Autentica il tuo dispositivo client e utilizza l’API DRM di Primetime, o l’API Primetime, per associare questo token a DRM di Primetime Cloud. In questo modo il dispositivo client invierà questo token di autenticazione a Primetime Cloud DRM insieme a tutte le richieste di licenza. Primetime Cloud DRM non elabora il token, ma lo trasmette invece (come BLOB opaco) all’endpoint BEES per l’elaborazione.
* **Licenze** - Richiedi una licenza per i contenuti protetti. Il dispositivo client aggiungerà automaticamente il token di autenticazione impostato in precedenza alla chiamata .
* **Diritto** - Primetime Cloud DRM determinerà che il contenuto è stato incluso in un pacchetto con un criterio che richiede API. Primetime Cloud DRM crea una richiesta JSON da inviare all’endpoint BEES. La risposta dell’API fornirà istruzioni a Primetime Cloud DRM sull’opportunità o meno di rilasciare una licenza e, facoltativamente, su quale criterio DRM utilizzare.

## Dettagli del flusso di lavoro dei criteri {#policy-workflow-details}

Quando Primetime Cloud DRM elabora una richiesta di licenza, analizza i criteri DRM nella richiesta per determinare se è necessaria una chiamata a un servizio di adesione di backend prima che sia possibile visualizzare il contenuto. Se una chiamata API *è* obbligatorio, Primetime Cloud DRM creerà la richiesta BEES, quindi analizza il criterio DRM per ottenere un endpoint URL API specifico per la richiesta BEES.

Applica il criterio DRM che indica il requisito BEES, specificando le due seguenti proprietà personalizzate nel criterio:

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Ad esempio, utilizzando Gestione criteri DRM di Primetime ( [!DNL AdobePolicyManager.jar]), specifica le due seguenti proprietà personalizzate nella [!DNL flashaccesstools.properties] file di configurazione:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Se utilizzi già `policy.customProp.1` o `policy.customProp.2` per un&#39;altra proprietà, è sufficiente utilizzare numeri univoci per le proprietà più recenti.

## Dettagli del flusso di lavoro del pacchetto {#package-workflow-details}

Durante la creazione del pacchetto dei contenuti protetti da Access Adobe, devi applicare al contenuto una delle policy DRM basate su BEES.

## Dettagli del flusso di lavoro di autenticazione {#authentication-workflow-details}

Affinché l&#39;endpoint BEES possa prendere decisioni sull&#39;adesione, il dispositivo client deve fornire informazioni sull&#39;autenticazione. Puoi eseguire questa operazione utilizzando un token di autenticazione specifico per il tuo cliente.

Primetime Cloud DRM non deve comprendere questo token, semplicemente passa questo token all&#39;endpoint BEES. Il dispositivo client è responsabile della creazione o dell’acquisizione di questo token e della sua impostazione tramite il `DRMManager.setAuthenticationToken()` API.

Per associare questo token a Primetime Cloud DRM , in modo che venga inviato alla richiesta di licenza:

Creare un&#39;istanza del `DRMManager` con i metadati DRM del contenuto che è stato incluso nel pacchetto per DRM di Primetime Cloud.

La `setAuthenticationToken()` Il metodo funziona associando l&#39;array di byte specificato all&#39;URL del server licenze fornito nei metadati DRM utilizzati per creare un&#39;istanza `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

Il token viene inviato con tutte le richieste di licenza finché il token non viene cancellato chiamando `.setAuthenticationToken` con null come parametro.

## Dettagli del flusso di lavoro della licenza{#license-workflow-details}

Richiedi una licenza da DRM di Primetime Cloud chiamando `mgr.loadVoucher()`.

## Dettagli della richiesta di adesione e della risposta{#entitlement-request-and-response-details}

Quando Primetime Cloud DRM determina che il contenuto è stato compilato con un criterio DRM consapevole dell&#39;API, costruisce la seguente richiesta JSON da inviare all&#39;endpoint BEES specificato nel criterio DRM:

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

La risposta seguente è prevista dall’endpoint BEES:

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

Primetime Cloud DRM utilizza la risposta per determinare se emettere o meno una licenza per il dispositivo richiedente e se deve sostituire una nuova policy DRM nel processo di generazione della licenza. Se `isAllowed` è `true` e non viene fornito alcun criterio nella risposta, quindi per generare la licenza verrà utilizzato il criterio DRM originale utilizzato durante il tempo di imballaggio del contenuto.
