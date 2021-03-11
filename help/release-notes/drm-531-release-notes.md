---
title: Note sulla versione di DRM 5.3.1
description: Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti in DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# Note sulla versione di DRM 5.3.1 {#drm-release-notes}

Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti in DRM 5.3.1.

## Nuove funzioni nella versione 5.3 {#new-features}

* **Interruzione sicura:** è possibile specificare se la riproduzione si arresta o continua alla fine di una finestra di riproduzione.
* **Protezione dell&#39;output basata sulla risoluzione (RBOP) -** È possibile specificare i vincoli di output in base alle risoluzioni dei pixel.
* **CDM Gating -** Per supportare HTML5, Adobe ha aggiornato il server della licenza di implementazione di riferimento incluso con l’SDK Java Adobe Primetime DRM (già Adobe Access DRM) per poter utilizzare tutti i messaggi di protocollo DRM in un singolo endpoint URL. Questo consolidamento dei metodi URL HTTP è necessario per rispettare la specifica EME HTML5 (Encrypted Media Extension) che a sua volta deve essere implementata dai fornitori DRM CDM (Content Decryption Module). In precedenza, questi erano gli unici endpoint URL esposti dal server licenze di implementazione di riferimento:

   * /flashaccess/i15n/v3 (Individualizzazione)
   * /flashaccess/license/v5 (Richiesta di licenza)
   * /flashaccess/licenseRet/v5 (ritorno della licenza)
   * /flashaccess/getServerVersion/v5 (Ottieni versione server)

Ora, tutte le richieste (provenienti da un CDM HTML5) possono essere indirizzate a un singolo endpoint: /req

Questa modifica è retrocompatibile con piattaforme non CDM, come Flash Player, Android, iOS.

* **Ridimensionamento RBOP -** Specifico dello spazio HTML5, RBOP contiene la funzionalità di downscaling automatico, dove se un bitrate che supera il bitrate consentito specificato nel criterio DRM, il contenuto verrà ridimensionato alla risoluzione massima consentita. Ad esempio, se un flusso 1080p viene inviato in streaming a un client che sta visualizzando il contenuto su un monitor non compatibile con HDCP, il criterio DRM può indicare che la risoluzione massima deve essere 720p. Primetime DRM decodifica il flusso 1080p e quindi lo ridimensiona a 720p prima di eseguirne il rendering sullo schermo. Se il browser che riproduce il video viene trascinato su un monitor che supporta HDCP, Primetime DRM smetterà di ridimensionare il contenuto e di riprodurlo a 1080.

## Problemi noti nella versione 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` restituisce i messaggi di log a  `flashaccess-global.log.`È necessario assicurarsi che il  `flashaccess-global.log` file si trovi nella stessa directory con Hasher.bat.

* L&#39;output di alcune delle `toJSON()`chiamate restituisce `Strings` che non sono completamente conformi a JSON o completamente conformi in modo stand alone (cioè, senza la composizione di strutture JSON).

* Il server chiavi Xbox accetta richieste chiave il cui valore di versione non è uguale a 1.

Il server chiavi Xbox dovrebbe supportare solo richieste chiave con versione uguale a 1, ma al momento il server accetta richieste chiave in cui la versione non è 1.

* Il server chiavi Xbox non convalida correttamente un criterio.

Il server chiavi Xbox non deve accettare criteri che non rientrano nella data di validità, ma attualmente il server li accetta indipendentemente.

* Il server chiavi Xbox deve rifiutare una richiesta chiave che contiene metadati creati con il certificato del packager errato.
* Il valore restituito di alcune strutture JSON non viene formattato correttamente per le classi relative alla protezione dell&#39;output basate sulla risoluzione.

Diverse classi implementano un metodo toJSON() che dovrebbe restituire una rappresentazione conforme a JSON dell&#39;oggetto come stringa, ma attualmente il valore restituito non è completamente conforme a JSON.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
