---
description: I gestori di funzioni fungono da wrapper intorno alla libreria TVSDK.
seo-description: I gestori di funzioni fungono da wrapper intorno alla libreria TVSDK.
seo-title: Struttura di implementazione di riferimento
title: Struttura di implementazione di riferimento
uuid: ae347a97-1500-476a-9fc8-c99e6b2ab8de
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Struttura di implementazione di riferimento {#reference-implementation-structure}

I gestori di funzioni fungono da wrapper intorno alla libreria TVSDK.

In Java, le classi sono strutturate in una gerarchia. Ad esempio, tutto il codice relativo all&#39;interfaccia utente in `com.adobe.primetime.reference.ui` e tutti i feature manager sono in `com.adobe.primetime.reference.manager`.

L&#39;implementazione di riferimento Primetime contiene i pacchetti seguenti:

| Pacchetto | Descrizione |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Questa classe estende android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contiene il codice per gli annunci personalizzati. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contiene il codice di interfaccia richiesto per la configurazione dei gestori di funzioni. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contiene le classi di supporto per DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Gli adattatori e gli adattatori per l&#39;interfaccia, la piattaforma e le informazioni di riferimento. Include inoltre il codice FeedAdapterFactory, ContentRenditionInfo e XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Fornisce classi per l&#39;accesso locale e remoto. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Qui troverete i manager delle funzioni e ManagerFactory. Per le funzioni facoltative attivabili o disattivabili, sono disponibili due gestori di funzioni: <ul><li>Un gestore di funzioni che rappresenta il nome della funzione, ad esempio CCManager. Questa funzionalità è disattivata e fornisce il comportamento predefinito di disattivazione.</li><li>Un gestore di funzioni che è stato aggiunto Attivato al nome del gestore di funzioni, ad esempio CCManagerOn. Questo Feature Manager fornisce un esempio di codice per la funzione abilitata.</li></ul> |
| [com.adobe.primetime.reference.ui.caalogo](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contiene il codice dell’interfaccia utente per il catalogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contiene il codice dell’interfaccia utente per il registro. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contiene il codice dell’interfaccia utente per il lettore. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contiene il codice dell’interfaccia utente per le impostazioni. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contiene classi di utilità generali. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contiene `HTTP-specific` classi di utilità. |
