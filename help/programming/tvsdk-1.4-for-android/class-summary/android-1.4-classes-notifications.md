---
description: Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che TVSDK genera ai fini della registrazione e del debug.
seo-description: Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che TVSDK genera ai fini della registrazione e del debug.
seo-title: Classi di notifica
title: Classi di notifica
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classi di notifica{#notification-classes}

Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che TVSDK genera ai fini della registrazione e del debug.

Pacchetto: Pacchetto [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) : [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Nome classe | Descrizione |
|---|---|
| MediaPlayerNotification. [Errore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | Classe che descrive la notifica di un errore che causa l&#39;interruzione della riproduzione del lettore. Si tratta di una notifica [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) di tipo ERROR. |
| MediaPlayerNotification. [Informazioni](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | Classe che descrive una notifica informativa. Si tratta di un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) di tipo di notifica INFO. |
| MediaPlayerNotification. [Avviso](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | Classe che descrive una notifica di avviso. Si tratta di una notifica [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) di tipo WARNING. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Incapsula la rappresentazione dell&#39;oggetto di un singolo evento di notifica all&#39;interno di [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Restituisce la descrizione associata al codice di notifica fornito. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | Classe che memorizza un registro di oggetti di notifica. Un elenco circolare di oggetti [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) che fornisce l&#39;accesso a un elenco cronologico eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un&#39;istanza separata della classe [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) . (nel pacchetto di [sessione](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) .) |
| NotificationHistory. [Elemento](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | Classe che definisce una voce nell&#39;elenco circolare in [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) e che contiene la notifica e la relativa marca temporale. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | Classe che contiene i tipi di notifiche supportati. |