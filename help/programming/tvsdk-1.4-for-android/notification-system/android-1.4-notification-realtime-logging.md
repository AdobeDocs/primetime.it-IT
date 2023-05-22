---
description: Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.
title: Aggiungere registrazione in tempo reale e debug
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Aggiungere registrazione in tempo reale e debug{#add-real-time-logging-and-debugging}

Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.

Il sistema di notifica consente di raccogliere le informazioni di registrazione e debug per la diagnostica e la convalida senza sovraccaricare il sistema.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non è previsto che gestisca il traffico con carichi elevati. Se l’implementazione non deve essere assolutamente completa, considera l’efficienza della trasmissione dei dati per evitare di sovraccaricare il sistema.

Di seguito è riportato un esempio di come recuperare le notifiche.

1. Crea un thread di esecuzione basato su timer per l’applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.

1. Se l&#39;intervallo del timer è troppo grande e la dimensione dell&#39;elenco eventi è troppo piccola, l&#39;elenco eventi di notifica verrà sottoposto a overflow. Per evitare questo overflow, eseguire una delle operazioni seguenti:

   * Diminuire l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   * Aumenta le dimensioni dell’elenco di notifiche.

1. Serializza le voci più recenti dell’evento di notifica in formato JSON e invia le voci a un server remoto per la post-elaborazione.

   Il server remoto potrebbe quindi visualizzare graficamente i dati forniti in tempo reale.
1. Per rilevare la perdita di eventi di notifica, cerca le lacune nella sequenza dei valori di indice degli eventi.

   Ogni evento di notifica ha un valore di indice che viene incrementato automaticamente da `session.NotificationHistory` classe.
