---
description: Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che TVSDK genera a scopo di registrazione e debug.
title: Classi di notifica
exl-id: 97a01418-f747-4a6e-bfa5-e680438e40c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Classi di notifica {#notification-classes}

Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che TVSDK genera a scopo di registrazione e debug.

| **Nome classe** | **Descrizione** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Classe che descrive la notifica di un errore che causa l’arresto della riproduzione da parte del lettore. Questo è un [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) del tipo di notifica ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Elenca tutte le notifiche inviate dal framework del lettore Primetime. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Incapsula la rappresentazione dell’oggetto di un singolo evento di notifica all’interno di [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Classe che memorizza un registro di oggetti di notifica [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) oggetti che consentono di accedere a un elenco di cronologia degli eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un’istanza separata del [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Classe che definisce una voce nell&#39;elenco circolare in [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) e contiene la notifica e la sua marca temporale. |
