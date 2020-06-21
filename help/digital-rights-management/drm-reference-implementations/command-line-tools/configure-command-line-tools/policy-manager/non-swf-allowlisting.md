---
seo-title: Elenco delle applicazioni non SWF consentite
title: Elenco delle applicazioni non SWF consentite
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Elenco delle applicazioni non SWF consentite {#non-swf-application-allowlisting}

AIR era la prima piattaforma che l’applicazione in uso consentiva l’elencazione e il nome della proprietà utilizzata per consentire l’elenco di applicazioni non SWF (Adobe AIR, iOS, Android, ecc.) conserva il nome originale: `policy.allowedAIRApplication.n`. Questo consente la riproduzione del contenuto da parte di tutte le applicazioni non Flash firmate con un certificato di firma prima della pubblicazione. Questo viene definito ID ** applicazione. Potete estrarre l&#39;ID applicazione utilizzando lo [!DNL AdobePublisherIDUtility.jar] strumento. Questo consente l&#39;inclusione nell&#39;elenco verrà applicata a qualsiasi client che supporta Primetime DRM.

L&#39;ID applicazione deriva dalla chiave pubblica del certificato di firma utilizzato per firmare una particolare applicazione. Se la chiave pubblica nel certificato scade mai, tutto il contenuto precedente consente la riproduzione nell&#39;elenco solo nelle app firmate con il vecchio certificato non verrà riprodotto nella nuova app (firmata con il nuovo certificato).

Se vi trovate in una situazione in cui disponete di una libreria di contenuti che consente di elencare le applicazioni firmate con un particolare certificato di firma, e tale certificato scade e vi viene rilasciato un nuovo certificato (con una diversa coppia di chiavi pubblica/privata), il contenuto precedente non verrà riprodotto nella nuova app *a meno che* non effettuiate una delle seguenti operazioni:

* Utilizzare un `PolicyUpdateList` server licenze per ignorare il criterio in entrata e inserire una nuova voce di elenco Consenti applicazione con il nuovo riepilogo del certificato di firma.
* Aggiornate la logica del server licenze in modo da ignorare il criterio in entrata e inserire una nuova voce di elenco Consentite applicazione.
* Richiedi all&#39;emittente del certificato di firma di emettere un nuovo certificato che utilizza la stessa coppia di chiavi pubblica/privata utilizzata dal certificato precedente.
* Se dovete distribuire contenuto HDS/HLS che fa riferimento a un endpoint URL per il recupero di tali informazioni, potete rigenerare il contenuto `DRMMetadata``DRMMetadata` (utilizzando l&#39;SDK Java DRM Java Primetime) per inserire un nuovo criterio DRM che contiene una voce di elenco Consenti applicazione aggiornata.

* Rifornisci tutto il contenuto precedente con un nuovo criterio DRM con il riepilogo del nuovo certificato di firma.

Per informazioni dettagliate, consultate `policy.allowedAIRApplication.n` in Proprietà *di* configurazione.

>[!NOTE]
>
>Per consentire l&#39;elencazione di un&#39;applicazione iOS è necessario un approccio speciale. Consultate [Consenti l&#39;elenco dell&#39;applicazione](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) iOS nella Guida *al programmatore* TVSDK per iOS.
