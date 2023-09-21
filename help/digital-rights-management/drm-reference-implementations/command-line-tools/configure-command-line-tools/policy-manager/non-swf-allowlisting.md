---
title: Inserimento di applicazioni non SWF nell’elenco Consentiti
description: Inserimento di applicazioni non SWF nell’elenco Consentiti
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Inserimento di applicazioni non SWF nell’elenco Consentiti {#non-swf-application-isting}

AIR è stata la prima piattaforma che presentava l’inserimento di applicazioni nell’elenco Consentiti e il nome della proprietà utilizzata per l’elenco consentiti di applicazioni non SWF (Adobe AIR, iOS, Android, ecc.) mantiene il nome originale: `policy.allowedAIRApplication.n`. Questo consente di riprodurre il contenuto da tutte le applicazioni non di Flash che sono firmate con un certificato di firma prima della pubblicazione. Tale procedura è denominata *ID applicazione*. È possibile estrarre l’ID applicazione utilizzando [!DNL AdobePublisherIDUtility.jar] strumento. Questo inserimento nell’elenco Consentiti verrà applicato a qualsiasi client che supporta Primetime DRM.

L’ID applicazione deriva dalla chiave pubblica del certificato di firma utilizzato per firmare una particolare applicazione. Se la chiave pubblica nel certificato scade, tutti i contenuti precedenti consentiranno la riproduzione solo sulle app firmate con il certificato precedente, ma non sulla nuova app (firmata con il nuovo certificato).

Se disponi di una libreria di contenuti che ti consente di elencare le applicazioni firmate con un determinato certificato di firma e tale certificato scade e ti viene rilasciato un nuovo certificato (con una coppia di chiavi pubblica/privata diversa), i contenuti precedenti non verranno riprodotti nella nuova app *salvo* effettua una delle seguenti operazioni:

* Utilizza un `PolicyUpdateList` sul server licenze per ignorare i criteri in ingresso e inserire una nuova voce di Elenco consentiti dell&#39;applicazione con il digest del nuovo certificato di firma.
* Aggiornare la logica del server licenze per ignorare il criterio in ingresso e inserire una nuova voce di Elenco consentiti dell&#39;applicazione.
* Richiedi che l’emittente del certificato di firma ti rilasci un nuovo certificato che utilizza la stessa coppia di chiavi pubblica/privata utilizzata nel certificato precedente.
* Se distribuisci contenuto HDS/HLS che fa riferimento a un endpoint URL per recuperare `DRMMetadata`, è possibile rigenerare `DRMMetadata` (utilizzando Primetime DRM Java SDK) per inserire un nuovo criterio DRM contenente una voce di Elenco consentiti Application aggiornata.

* Riconfezionate tutti i vecchi contenuti con un nuovo criterio DRM con il digest del nuovo certificato di firma.

Consulta `policy.allowedAIRApplication.n` in *Proprietà di configurazione* per i dettagli.

>[!NOTE]
>
>Per inserire un’applicazione iOS nell’elenco Consentiti è necessario un approccio speciale. Consulta [Elenco consentiti dell’applicazione iOS](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) nel *Guida per i programmatori di TVSDK per iOS*.
