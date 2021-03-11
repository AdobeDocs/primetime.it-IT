---
description: Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che TVSDK genera a scopo di log e debug.
title: Classi di notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Classi di notifica{#notification-classes}

Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che TVSDK genera a scopo di log e debug.

Pacchetto: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) Pacchetto: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Nome classe | Descrizione |
|---|---|
| MediaPlayerNotification. [Errore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | Classe che descrive la notifica di un errore che causa l&#39;arresto della riproduzione del lettore. Si tratta di un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) del tipo di notifica ERROR. |
| MediaPlayerNotification. [Info](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | Classe che descrive una notifica informativa. Si tratta di un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) del tipo di notifica INFO. |
| MediaPlayerNotification. [Avviso](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | Classe che descrive una notifica di avviso. Si tratta di un [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) del tipo di notifica WARNING. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Racchiude la rappresentazione dell&#39;oggetto di un singolo evento di notifica all&#39;interno di [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Restituisce la descrizione associata al codice di notifica fornito. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | Classe che memorizza un registro degli oggetti di notifica. Elenco circolare di oggetti [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) che consente di accedere a un elenco di cronologia degli eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un&#39;istanza separata della classe [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) . (Nel pacchetto [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) ). |
| NotificationHistory. [Elemento](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | Classe che definisce una voce nell&#39;elenco circolare in [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) e che contiene la notifica e la relativa marca temporale. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | Classe che contiene i tipi di notifiche supportati. |