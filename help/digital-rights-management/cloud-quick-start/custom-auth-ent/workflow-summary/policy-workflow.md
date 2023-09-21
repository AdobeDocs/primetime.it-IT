---
title: Dettagli flusso di lavoro criteri
description: Dettagli flusso di lavoro criteri
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Flusso di lavoro API {#bees-workflow}

**Riepilogo:**

* **Policy** - Creare una policy DRM in grado di riconoscere le API che indichi che le API sono necessarie per tutti i contenuti inclusi in questo criterio.
* **Imballaggio** - Contenuto del pacchetto utilizzando la policy DRM in grado di riconoscere le API.
* **Autenticazione** : autentica il dispositivo client e utilizza l’API DRM di Primetime o l’API di Primetime per associare questo token a Cloud DRM di Primetime. In questo modo il dispositivo client invierà questo token di autenticazione a Primetime Cloud DRM insieme a tutte le richieste di licenza. Primetime Cloud DRM non elabora il token, ma lo trasmette (come BLOB opaco) all’endpoint BEES per l’elaborazione.
* **Licenze** - Richiedi una licenza per il contenuto protetto. Il dispositivo client aggiungerà automaticamente alla chiamata il token di autenticazione impostato in precedenza.
* **Diritto** - Primetime Cloud DRM determinerà che il contenuto è stato compilato con un criterio che richiede BEES. Primetime Cloud DRM creerà una richiesta JSON da inviare all’endpoint BEES. La risposta di BEES indicherà a Primetime Cloud DRM se rilasciare o meno una licenza e, facoltativamente, quali criteri DRM utilizzare.

## Dettagli flusso di lavoro criteri {#policy-workflow-details}

Quando Primetime Cloud DRM elabora una richiesta di licenza, analizza i criteri DRM nella richiesta per determinare se è necessaria una chiamata a un servizio di adesione back-end prima che sia possibile visualizzare il contenuto. Se un’API chiama *è* Obbligatorio, Primetime Cloud DRM creerà la richiesta BEES, quindi analizzerà i criteri DRM per ottenere un endpoint URL BEES specifico per la richiesta BEES.

Applicare la regola DRM che indica il requisito BEES, specificando le due proprietà personalizzate seguenti nel criterio:

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Ad esempio, utilizzando Primetime DRM Policy Manager ( [!DNL AdobePolicyManager.jar]), puoi specificare le due seguenti proprietà personalizzate nel [!DNL flashaccesstools.properties] file di configurazione:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Se utilizzi già `policy.customProp.1` o `policy.customProp.2` per un’altra proprietà, utilizza semplicemente numeri univoci per le proprietà più recenti.

## Dettagli del flusso di lavoro del pacchetto {#package-workflow-details}

Durante la creazione della confezione del contenuto protetto dall’accesso Adobe, è necessario applicare al contenuto uno dei criteri DRM in grado di riconoscere le API.

## Dettagli del flusso di lavoro di autenticazione {#authentication-workflow-details}

Affinché l’endpoint BEES possa prendere decisioni in merito all’adesione, il dispositivo client deve fornire informazioni di autenticazione. A tale scopo, utilizza un token di autenticazione personalizzato specifico per il cliente.

Primetime Cloud DRM non deve necessariamente comprendere questo token, ma lo trasmette semplicemente all’endpoint BEES. Il dispositivo client è responsabile della creazione o dell’acquisizione di questo token e della sua impostazione utilizzando `DRMManager.setAuthenticationToken()` API.

Per associare questo token a Primetime Cloud DRM, in modo che venga inviato con la richiesta di licenza, effettuare le seguenti operazioni:

Crea un&#39;istanza di `DRMManager` oggetto con i metadati DRM del contenuto incluso nel pacchetto per Primetime Cloud DRM.

Il `setAuthenticationToken()` Il metodo funziona associando la matrice di byte specificata all&#39;URL del server licenze fornito nei metadati DRM utilizzati per creare un&#39;istanza `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

Il token viene inviato con tutte le richieste di licenza fino a quando non viene cancellato chiamando `.setAuthenticationToken` con null come parametro.

## Dettagli del flusso di lavoro della licenza{#license-workflow-details}

Richiedi una licenza da Primetime Cloud DRM chiamando `mgr.loadVoucher()`.

## Dettagli della richiesta di adesione e della risposta{#entitlement-request-and-response-details}

Quando Primetime Cloud DRM determina che il contenuto è stato compilato con un criterio DRM in base alle API, crea la seguente richiesta JSON da inviare all’endpoint BEES specificato nel criterio DRM:

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

Si prevede la seguente risposta dall’endpoint BEES:

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

Primetime Cloud DRM utilizza la risposta per determinare se deve o meno rilasciare una licenza al dispositivo richiedente e se deve sostituire un nuovo criterio DRM nel processo di generazione delle licenze. Se `isAllowed` è `true` e non viene fornito alcun criterio nella risposta, per generare la licenza verrà utilizzato il criterio DRM originale utilizzato durante il tempo di creazione del contenuto.
