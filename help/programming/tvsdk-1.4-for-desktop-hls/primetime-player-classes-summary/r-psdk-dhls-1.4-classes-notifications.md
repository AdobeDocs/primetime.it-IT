---
description: Queste classi descrivono i messaggi relativi a errori, avvisi e ad alcune attività che presentano problemi di registrazione e debug.
title: Classi di notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Classi di notifica {#notification-classes}

Queste classi descrivono i messaggi relativi a errori, avvisi e ad alcune attività che presentano problemi di registrazione e debug.

Pacchetto: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nome classe | Descrizione |
|---|---|
| [Notifica](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Racchiude la rappresentazione dell&#39;oggetto di un singolo evento di notifica all&#39;interno di [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Restituisce la descrizione associata al codice di notifica fornito e fornisce costanti numeriche per gli oggetti di notifica. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Classe che memorizza un registro degli oggetti di notifica. Elenco circolare di oggetti [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) che consente di accedere a un elenco di cronologia degli eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un&#39;istanza separata della classe [Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) . |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Classe che definisce una voce nell&#39;elenco circolare in [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) e che contiene la notifica e la relativa marca temporale. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Classe che contiene i tipi di notifiche supportati. |

