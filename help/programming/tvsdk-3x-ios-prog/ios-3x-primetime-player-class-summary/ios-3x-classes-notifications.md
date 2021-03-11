---
description: Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che TVSDK genera a scopo di log e debug.
title: Classi di notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Classi di notifica {#notification-classes}

Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che TVSDK genera a scopo di log e debug.

| **Nome classe** | **Descrizione** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Classe che descrive la notifica di un errore che causa l&#39;arresto della riproduzione del lettore. Si tratta di un [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo di notifica ERROR. |
| [Notifiche di PTMediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Elenca tutte le notifiche inviate dal framework di Primetime Player. |
| [Notifica PTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Racchiude la rappresentazione dell&#39;oggetto di un singolo evento di notifica all&#39;interno di [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Classe che memorizza un registro di oggetti di notifica [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) oggetti che fornisce l&#39;accesso a un elenco di cronologia eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un&#39;istanza separata del [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Classe che definisce una voce nell&#39;elenco circolare in [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) e contiene la notifica e la relativa marca temporale. |

