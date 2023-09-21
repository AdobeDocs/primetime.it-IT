---
description: Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che generano problemi a scopo di registrazione e debug.
title: Classi di notifica
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Classi di notifica {#notification-classes}

Queste classi descrivono i messaggi relativi a errori, avvisi e alcune attività che generano problemi a scopo di registrazione e debug.

Pacchetto [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nome classe | Descrizione |
|---|---|
| [Notifica](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Classe che fornisce messaggi informativi, avvisi ed errori. Incapsula la rappresentazione dell’oggetto di un singolo evento di notifica all’interno di [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Restituisce la descrizione associata al codice di notifica fornito e fornisce costanti numeriche per gli oggetti di notifica. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Classe che memorizza un registro di oggetti di notifica. Un elenco circolare di [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) oggetti che consentono di accedere a un elenco di cronologia degli eventi di notifica. In altre parole, mantiene un elenco di elementi, ogni elemento contenente un’istanza separata del [Notifica](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) classe. |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Classe che definisce una voce nell&#39;elenco circolare in [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) e contiene la notifica e la sua marca temporale. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Classe contenente i tipi di notifiche supportati. |
