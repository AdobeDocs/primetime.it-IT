---
description: Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che TVSDK genera ai fini della registrazione e del debug.
seo-description: Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che TVSDK genera ai fini della registrazione e del debug.
seo-title: Classi di notifica
title: Classi di notifica
uuid: 8a276056-775f-432d-a4b4-722f6e4e278f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Classi di notifica {#notification-classes}

Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che TVSDK genera ai fini della registrazione e del debug.

| **Nome classe** | **Descrizione** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Classe che descrive la notifica di un errore che causa l&#39;interruzione della riproduzione del lettore. Si tratta di una notifica [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo di notifica ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Elenca tutte le notifiche inviate dal framework Primetime Player. |
| [PTNotificazione](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Incapsula la rappresentazione dell&#39;oggetto di un singolo evento di notifica all&#39;interno di [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Classe che memorizza un registro di oggetti di notifica oggetti [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) che fornisce l&#39;accesso a un elenco cronologico eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un&#39;istanza separata dell&#39; [avviso PTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Classe che definisce una voce nell&#39;elenco circolare in [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) e che contiene la notifica e la relativa marca temporale. |

