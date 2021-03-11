---
title: Elenco Consentiti applicazioni non SWF
description: Elenco Consentiti applicazioni non SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Elenco consentiti applicazioni non SWF {#non-swf-application-isting}

AIR è stata la prima piattaforma che presentava l’applicazione allow listing, e il nome della proprietà utilizzata per elenco consentiti di applicazioni non SWF (Adobe AIR, iOS, Android, ecc.) conserva il nome originale: `policy.allowedAIRApplication.n`. Questo consente la riproduzione del contenuto da parte di tutte le applicazioni non Flash firmate con un certificato di firma prima della pubblicazione. Questo viene indicato come *ID applicazione*. Puoi estrarre l’ID applicazione utilizzando lo strumento [!DNL AdobePublisherIDUtility.jar] . L’inserimento nell’elenco Consentiti verrà applicato a qualsiasi client che supporti DRM di Primetime.

L&#39;ID applicazione deriva dalla chiave pubblica del certificato di firma utilizzato per firmare una particolare applicazione. Se la chiave pubblica nel certificato scade, tutti i contenuti precedenti consentono di riprodurre nell’elenco solo le app firmate con il certificato precedente e non vengono riprodotti nella nuova app (firmata con il nuovo certificato).

Se ti trovi nella situazione in cui disponi di una libreria di contenuti per l’elenco delle applicazioni firmate con un particolare certificato di firma e tale certificato scade e ti viene rilasciato un nuovo certificato (con una diversa coppia di chiavi pubblica/privata), il contenuto precedente non verrà riprodotto nella nuova app *a meno che* non esegua una delle seguenti operazioni:

* Utilizzare un `PolicyUpdateList` sul server licenze per ignorare i criteri in entrata e inserire una nuova voce di Elenco consentiti applicazione con il riepilogo del nuovo certificato di firma .
* Aggiornare la logica del server licenze per ignorare il criterio in entrata e inserire una nuova voce di Elenco consentiti applicazione.
* Richiedi all’emittente del certificato di firma di emettere un nuovo certificato che utilizza la stessa coppia di chiavi pubblica/privata utilizzata dal certificato precedente.
* Se distribuisci contenuto HDS/HLS che fa riferimento a un endpoint URL per il recupero di `DRMMetadata`, puoi rigenerare il `DRMMetadata` (utilizzando l&#39;SDK Java DRM di Primetime) per inserire un nuovo criterio DRM contenente una voce di Elenco consentiti dell&#39;applicazione aggiornata.

* Ricompila tutti i contenuti obsoleti con un nuovo criterio DRM con il riepilogo del nuovo certificato di firma.

Per ulteriori informazioni, consulta `policy.allowedAIRApplication.n` in *Proprietà di configurazione* .

>[!NOTE]
>
>L’inserimento di un’applicazione iOS nell’elenco Consentiti richiede un approccio speciale. Consulta [Elenco consentiti l&#39;applicazione iOS](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) nella *Guida TVSDK per programmatori iOS*.
