---
description: Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che presentano problemi di accesso e debug.
seo-description: Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che presentano problemi di accesso e debug.
seo-title: Classi di notifica
title: Classi di notifica
uuid: 3befc64b-4abd-47df-9c45-215b49029757
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Classi di notifica {#notification-classes}

Queste classi descrivono i messaggi di errore, gli avvisi e alcune attività che presentano problemi di accesso e debug.

Pacchetto: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nome classe | Descrizione |
|---|---|
| [Notifica](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Incapsula la rappresentazione dell&#39;oggetto di un singolo evento di notifica all&#39;interno di [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Restituisce la descrizione associata al codice di notifica fornito e fornisce costanti numeriche per gli oggetti di notifica. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Classe che memorizza un registro di oggetti di notifica. Un elenco circolare di oggetti [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) che fornisce l&#39;accesso a un elenco cronologico eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un&#39;istanza separata della classe [Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html). |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Classe che definisce una voce nell&#39;elenco circolare in [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) e che contiene la notifica e la relativa marca temporale. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Classe che contiene i tipi di notifiche supportati. |

