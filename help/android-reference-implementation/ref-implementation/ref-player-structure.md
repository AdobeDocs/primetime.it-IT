---
description: I gestori di funzioni fungono da wrapper per la libreria TVSDK.
title: Struttura di implementazione di riferimento
exl-id: cf102ccc-2e31-4197-a321-e485f77ba754
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Struttura di implementazione di riferimento {#reference-implementation-structure}

I gestori di funzioni fungono da wrapper per la libreria TVSDK.

In Java, le classi sono strutturate in una gerarchia. Ad esempio, tutto il codice relativo all’interfaccia utente in `com.adobe.primetime.reference.ui` e tutti i gestori di funzionalità si trovano in `com.adobe.primetime.reference.manager`.

L’implementazione di riferimento di Primetime contiene i seguenti pacchetti:

| Pacchetto | Descrizione |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Questa classe estende android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contiene il codice per gli annunci personalizzati. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contiene il codice di interfaccia necessario per la configurazione dei gestori di funzionalità. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contiene classi di supporto per DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adattatori e adattatori di elementi per informazioni su interfaccia, piattaforma e riferimento. Include inoltre il codice FeedAdapterFactory, ContentRenditionInfo e XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Fornisce classi per la registrazione locale e remota. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Qui è possibile trovare i gestori di funzionalità e ManagerFactory. Per le funzioni facoltative che possono essere attivate o disattivate, sono disponibili due gestori di funzioni: <ul><li>Un gestore di funzionalità che è il nome della funzionalità, ad esempio CCManager. Questa funzione di gestione è disattivata e fornisce il comportamento predefinito di disattivazione.</li><li>Un gestore di funzioni che ha On aggiunto al nome del gestore di funzioni, ad esempio CCManagerOn. Questo gestore di funzioni fornisce un codice di esempio per la funzione abilitata.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contiene il codice dell’interfaccia utente per il catalogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contiene il codice dell’interfaccia utente per il registro. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contiene il codice dell’interfaccia utente del lettore. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contiene il codice dell’interfaccia utente per le impostazioni di. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contiene le classi di utilità generali. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contiene `HTTP-specific` classi di utilità. |
