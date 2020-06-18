---
seo-title: Whitelist delle applicazioni non SWF
title: Whitelist delle applicazioni non SWF
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Whitelist delle applicazioni non SWF {#non-swf-application-whitelisting}

AIR è stata la prima piattaforma che presentava la whitelist dell’applicazione e il nome della proprietà utilizzata per inserire in una whitelist le applicazioni non SWF (Adobe AIR, iOS, Android, ecc.) conserva il nome originale: `policy.allowedAIRApplication.n`. Questo consente la riproduzione del contenuto da parte di tutte le applicazioni non Flash firmate con un certificato di firma prima della pubblicazione. Questo viene definito ID ** applicazione. Potete estrarre l&#39;ID applicazione utilizzando lo [!DNL AdobePublisherIDUtility.jar] strumento. Questa whitelist verrà applicata a qualsiasi client che supporta DRM di Primetime.

L&#39;ID applicazione deriva dalla chiave pubblica del certificato di firma utilizzato per firmare una particolare applicazione. Se la chiave pubblica nel certificato scade mai, tutto il contenuto precedente inserito nella lista bianca per essere riprodotto solo sulle app firmate con il vecchio certificato non verrà riprodotto nella nuova app (firmata con il nuovo certificato).

Se si è in una situazione in cui si dispone di una libreria di contenuto inserita nella lista bianca per le applicazioni firmate con un particolare certificato di firma, tale certificato scade e si ottiene un nuovo certificato (con una diversa coppia di chiavi pubblica/privata), il contenuto precedente non verrà riprodotto nella nuova app *a meno che* non si effettui una delle seguenti operazioni:

* Utilizzare un `PolicyUpdateList` server licenze per ignorare il criterio in entrata e inserire una nuova voce Whitelist applicazione con il nuovo riepilogo del certificato di firma.
* Aggiornate la logica del server licenze per ignorare il criterio in entrata e inserire una nuova voce Whitelist dell&#39;applicazione.
* Richiedi all&#39;emittente del certificato di firma di emettere un nuovo certificato che utilizza la stessa coppia di chiavi pubblica/privata utilizzata dal certificato precedente.
* Se distribuite contenuto HDS/HLS che fa riferimento a un endpoint URL per il recupero del `DRMMetadata`, potete rigenerare il contenuto `DRMMetadata` (utilizzando l&#39;SDK Java DRM di Primetime) per inserire un nuovo criterio DRM che contiene una voce Whitelist di applicazione aggiornata.

* Rifornisci tutto il contenuto precedente con un nuovo criterio DRM con il riepilogo del nuovo certificato di firma.

Per informazioni dettagliate, consultate `policy.allowedAIRApplication.n` in Proprietà *di* configurazione.

>[!NOTE]
>
>Per consentire l&#39;elencazione di un&#39;applicazione iOS è necessario un approccio speciale. Consultate [Consenti l&#39;elenco dell&#39;applicazione](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) iOS nella Guida *al programmatore* TVSDK per iOS.
