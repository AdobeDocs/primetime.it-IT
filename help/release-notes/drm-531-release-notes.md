---
title: Note sulla versione di DRM 5.3.1
seo-title: Note sulla versione di DRM 5.3.1
description: Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti di DRM 5.3.1.
seo-description: Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti di DRM 5.3.1.
uuid: bb61b79f-a5b3-42ed-8016-495b1ac99ea6
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Note sulla versione di DRM 5.3.1 {#drm-release-notes}

Le note sulla versione di DRM 5.3.1 descrivono le nuove funzioni e i problemi noti di DRM 5.3.1.

## Nuove funzioni nella versione 5.3 {#new-features}

* **Arresto sicuro -** È possibile specificare se la riproduzione si arresta o continua alla fine di una finestra di riproduzione.
* **Protezione dell&#39;output basata sulla risoluzione (RBOP) -** È possibile specificare i vincoli di output in base alle risoluzioni dei pixel.
* **CDM Gating -** Per supportare HTML5,  Adobe ha aggiornato il server delle licenze di implementazione di riferimento incluso con l’SDK Java  Adobe Primetime DRM (già  Adobe accesso  ad Access DRM) per poter utilizzare tutti i messaggi del protocollo DRM in un singolo endpoint URL. Questo consolidamento dei metodi URL HTTP è necessario per conformarsi alla specifica HTML5 EME (Encrypted Media Extension) richiesta a sua volta dai fornitori DRM CDM (Content Decryption Module). Precedentemente, questi erano gli unici endpoint URL esposti dal server licenze di implementazione di riferimento:

   * /flashaccess/i15n/v3 (Individualizzazione)
   * /flashaccess/license/v5 (richiesta di licenza)
   * /flashaccess/licenseRet/v5 (restituzione licenza)
   * /flashaccess/getServerVersion/v5 (Ottieni versione server)

Ora, tutte le richieste (provenienti da un CDM HTML5) possono essere indirizzate a un singolo endpoint: /req

Questa modifica è compatibile con le piattaforme non CDM, come Flash Player, Android, iOS.

* **Ridimensionamento RBOP -** Specifico per lo spazio HTML5, RBOP contiene la funzionalità di downscaling automatico, dove se un bitrate supera il bitrate consentito specificato nel criterio DRM, il contenuto verrà ridotto alla risoluzione massima consentita. Ad esempio, se un flusso 1080p viene inviato in streaming a un client che sta visualizzando il contenuto su un monitor non conforme con HDCP, il criterio DRM potrebbe indicare che la risoluzione massima deve essere 720p. Primetime DRM deciderà il flusso 1080p e lo ridurrà a 720p prima di renderlo disponibile sullo schermo. Se il browser che riproduce il video viene trascinato su un monitor che supporta HDCP, Primetime DRM interrompe il downscaling dei contenuti e consente la riproduzione a 1080.

## Problemi noti nella versione 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` invia messaggi di registro a  `flashaccess-global.log.`È necessario assicurarsi che il  `flashaccess-global.log` file si trovi nella stessa directory con Hasher.bat.

* L&#39;output di alcune delle `toJSON()`chiamate restituiscono `Strings` che non sono completamente conformi a JSON o pienamente conformi in modo autonomo (ovvero, senza la composizione di strutture JSON).

* Il server chiavi Xbox accetta richieste chiave il cui valore di versione non è uguale a 1.

Il server chiavi Xbox dovrebbe supportare solo le richieste chiave con una versione uguale a 1, ma al momento il server accetta richieste chiave in cui la versione non è 1.

* Il server chiavi Xbox non convalida correttamente un criterio.

Il server chiavi Xbox non deve accettare criteri che non rientrano nella data di validità, ma al momento, il server li accetta indipendentemente.

* Il server chiavi Xbox deve rifiutare una richiesta di chiave che contiene i metadati creati con un certificato Packager errato.
* Il valore restituito di alcune strutture JSON non è formattato correttamente per le classi correlate alla protezione dell&#39;output basate sulla risoluzione.

Diverse classi implementano un metodo toJSON() che dovrebbe restituire una rappresentazione conforme a JSON dell&#39;oggetto come stringa, ma al momento il valore restituito non è completamente conforme a JSON.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida in linea alla pagina [ Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
