---
seo-title: Dettagli del flusso di lavoro dei criteri
title: Dettagli del flusso di lavoro dei criteri
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# BEES Workflow {#bees-workflow}

**Riepilogo:**

* **Criterio** - Crea un criterio basato su DRM che indichi che BEES è richiesto per tutti i contenuti inclusi in un pacchetto utilizzando questo criterio.
* **Creazione di pacchetti** - Creazione di pacchetti di contenuti tramite la politica DRM basata su BEES.
* **Autenticazione** : autenticate il dispositivo client e utilizzate l&#39;API DRM di Primetime, o l&#39;API Primetime, per associare questo token a DRM di Primetime Cloud. In questo modo il dispositivo client invierà il token di autenticazione a Primetime Cloud DRM insieme a tutte le richieste di licenza. Primetime Cloud DRM non elaborerà il token, ma lo trasmetterà (come bobina opaca) all&#39;endpoint BEES per l&#39;elaborazione.
* **Licenze** - Richiedi una licenza per il contenuto protetto. Il dispositivo client aggiungerà automaticamente il token di autenticazione precedentemente impostato alla chiamata.
* **Adesione** - Primetime Cloud DRM determinerà che il contenuto è stato incluso in un pacchetto con un criterio che richiede BEES. Primetime Cloud DRM crea una richiesta JSON da inviare all’endpoint BEES. La risposta di BEES indicherà a Primetime Cloud DRM se rilasciare o meno una licenza e, facoltativamente, quale criterio DRM utilizzare.

## Dettagli del flusso di lavoro dei criteri {#policy-workflow-details}

Quando Primetime Cloud DRM elabora una richiesta di licenza, analizza il criterio DRM nella richiesta per determinare se è necessaria una chiamata a un servizio di adesione backend prima che sia possibile visualizzare il contenuto. Se *è* richiesta una chiamata API, Primetime Cloud DRM creerà la richiesta BEES, quindi analizzerà il criterio DRM per ottenere un endpoint URL API specificato per la richiesta BEES.

Applicate il criterio DRM che indica il requisito BEES, specificando le due seguenti proprietà personalizzate nel criterio:

    * `policy.customProp.1=api.Required=&lt;true| false>`
    * `policy.customProp.2=bees.url=&lt;url dell&#39;endpoint BEES>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Ad esempio, utilizzando Primetime DRM Policy Manager ( [!DNL AdobePolicyManager.jar]), è possibile specificare le due proprietà personalizzate seguenti nel file di [!DNL flashaccesstools.properties] configurazione:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Se si sta già utilizzando `policy.customProp.1` o `policy.customProp.2` per un&#39;altra proprietà, è sufficiente utilizzare numeri univoci per le proprietà più recenti.

## Dettagli del flusso di lavoro del pacchetto {#package-workflow-details}

Durante la creazione del pacchetto dei contenuti protetti da Adobe Access, è necessario applicare al contenuto uno dei criteri DRM compatibili con le API.

## Dettagli del flusso di lavoro di autenticazione {#authentication-workflow-details}

Affinché l&#39;endpoint BEES possa prendere decisioni sull&#39;adesione, il dispositivo client deve fornire informazioni sull&#39;autenticazione. A tal fine, utilizzate un token di autenticazione specifico per il cliente.

Primetime Cloud DRM non deve comprendere questo token; passa semplicemente questo token all’endpoint BEES. Il dispositivo client è responsabile della creazione o acquisizione del token e della relativa impostazione tramite l&#39; `DRMManager.setAuthenticationToken()` API.

Per associare questo token a DRM di Primetime Cloud, effettuate le seguenti operazioni in modo che venga inviato con la richiesta di licenza:

Create un&#39;istanza dell&#39; `DRMManager` oggetto con i metadati DRM del contenuto incluso nel pacchetto per DRM di Primetime Cloud.

Il `setAuthenticationToken()` metodo funziona associando l&#39;array di byte specificato all&#39;URL del server licenze fornito nei metadati DRM utilizzati per creare un&#39;istanza `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

Il token viene inviato con tutte le richieste di licenza finché il token non viene cancellato chiamando `.setAuthenticationToken` con null come parametro.

## Dettagli del flusso di lavoro della licenza{#license-workflow-details}

Richiedi una licenza da Primetime Cloud DRM chiamando `mgr.loadVoucher()`.

## Dettagli richiesta di adesione e risposta{#entitlement-request-and-response-details}

Quando Primetime Cloud DRM determina che il contenuto è stato incluso in un pacchetto con un criterio DRM basato su BEES, crea la seguente richiesta JSON da inviare all&#39;endpoint BEES specificato nel criterio DRM:

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

Primetime Cloud DRM utilizza la risposta per determinare se rilasciare o meno una licenza al dispositivo richiedente e se sostituire una nuova policy DRM nel processo di generazione della licenza. Se `isAllowed` è `true` e non viene fornito alcun criterio nella risposta, per generare la licenza verrà utilizzato il criterio DRM originale utilizzato durante il tempo di creazione del pacchetto di contenuto.