---
description: I gestori di funzioni fungono da wrapper intorno alla libreria TVSDK.
title: Struttura di implementazione di riferimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Struttura di implementazione di riferimento {#reference-implementation-structure}

I gestori di funzioni fungono da wrapper intorno alla libreria TVSDK.

In Java, le classi sono strutturate in una gerarchia. Ad esempio, tutto il codice relativo all’interfaccia utente in `com.adobe.primetime.reference.ui` e tutti i gestori di funzioni si trovano in `com.adobe.primetime.reference.manager`.

L&#39;implementazione di riferimento di Primetime contiene i seguenti pacchetti:

| Pacchetto | Descrizione |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Questa classe estende android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contiene il codice per gli annunci personalizzati. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contiene il codice di interfaccia necessario per configurare i gestori di funzioni. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contiene classi di supporto per DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adattatori e adattatori per l&#39;interfaccia, la piattaforma e le informazioni di riferimento. Sono inclusi anche i codici FeedAdapterFactory, ContentRenditionInfo e XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Fornisce classi per la registrazione locale e remota. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Qui è possibile trovare i gestori di funzioni e ManagerFactory. Per le funzioni facoltative attivabili o disattivabili, sono disponibili due gestori di funzioni: <ul><li>Un feature manager che rappresenta il nome della feature, ad esempio CCManager. Questo feature manager è disattivato e fornisce il comportamento predefinito di disattivazione.</li><li>Un feature manager aggiunto al nome del feature manager, ad esempio CCManagerOn. Questo feature manager fornisce un codice di esempio per la funzione abilitata.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contiene il codice dell’interfaccia utente per il catalogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contiene il codice dell’interfaccia utente per il registro. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contiene il codice dell&#39;interfaccia utente per il lettore. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contiene il codice dell&#39;interfaccia utente per le impostazioni. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contiene classi di utilità generali. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contiene le classi di utilità `HTTP-specific`. |
