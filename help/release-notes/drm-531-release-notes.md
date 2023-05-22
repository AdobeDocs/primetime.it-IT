---
title: Note sulla versione di DRM 5.3.1
description: Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti di DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: e4e0a933-cfc6-4713-ae13-5df11cfc1aad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Note sulla versione di DRM 5.3.1 {#drm-release-notes}

Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti di DRM 5.3.1.

## Nuove funzioni nella versione 5.3 {#new-features}

* **Arresto sicuro -** È possibile specificare se la riproduzione si arresta o continua alla fine di una finestra di riproduzione.
* **Protezione dell&#39;output basata sulla risoluzione (RBOP)** Potete specificare i vincoli di output in base alle risoluzioni in pixel.
* **Gating CDM -** Per supportare HTML5, Adobe ha aggiornato il server licenze di implementazione di riferimento incluso nell’SDK Java Adobe Primetime DRM (precedentemente Adobe Access DRM) per poter utilizzare tutti i messaggi del protocollo DRM a un singolo endpoint URL. Questo consolidamento dei metodi URL HTTP è necessario per rispettare la specifica HTML5 EME (Encrypted Media Extension) che a sua volta deve essere implementata dai fornitori di DRM CDM (Content Decryption Module). In precedenza, questi erano gli unici endpoint URL esposti dal server licenze di implementazione di riferimento:

   * /flashaccess/i15n/v3 (Personalizzazione)
   * /flashaccess/license/v5 (Richiesta licenza)
   * /flashaccess/licenseRet/v5 (ritorno licenza)
   * /flashaccess/getServerVersion/v5 (Ottieni versione server)

Ora, tutte le richieste (provenienti da un CDM HTML5) possono essere indirizzate a un singolo endpoint: /req

Questa modifica è compatibile con le versioni precedenti di piattaforme non CDM, come Flash Player, Android e iOS.

* **Riduzione RBOP -** Specifico per lo spazio HTML5, RBOP contiene la funzionalità di downscaling automatico, in cui se un bitrate che supera il bitrate consentito specificato nel criterio DRM, il contenuto verrà downscalato alla risoluzione massima consentita. Ad esempio, se un flusso 1080p viene inviato a un client che visualizza il contenuto su un monitor non compatibile HDCP, la regola DRM potrebbe indicare che la risoluzione massima dovrebbe essere 720p. Primetime DRM decodificherà il flusso 1080p e quindi lo ridurrà a 720p prima di eseguirne il rendering sullo schermo. Se il browser che riproduce il video viene quindi trascinato su un monitor che non supporta HDCP, Primetime DRM interrompe il downscaling del contenuto e consente la riproduzione a 1080.

## Problemi noti nella versione 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` invia messaggi di registro a `flashaccess-global.log.`È necessario assicurarsi che `flashaccess-global.log` Il file si trova nella stessa directory di Hasher.bat.

* L&#39;output di alcuni dei `toJSON()`chiamate restituite `Strings` che non sono pienamente conformi JSON o pienamente conformi in modo autonomo (ovvero, senza la composizione di strutture JSON).

* Il server della chiave Xbox accetta richieste chiave il cui valore di versione non è uguale a 1.

Il server della chiave Xbox deve supportare solo le richieste chiave con versione uguale a 1, ma attualmente il server accetta le richieste chiave se la versione non è 1.

* Il server della chiave Xbox non convalida correttamente una policy.

Il server della chiave Xbox non deve accettare criteri che non rientrano nella data di validità, ma attualmente li accetta indipendentemente.

* Il server della chiave Xbox deve rifiutare una richiesta chiave contenente metadati creati con un certificato Packager errato.
* Il valore restituito di alcune strutture JSON non viene formattato correttamente per le classi correlate alla protezione output basata sulla risoluzione.

Diverse classi implementano un metodo toJSON() che deve restituire una rappresentazione conforme a JSON di tale oggetto come String, ma attualmente il valore restituito non è completamente conforme a JSON.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
