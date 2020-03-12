---
description: Potete utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.
seo-description: Potete utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.
seo-title: Aggiunta di registrazioni e debugging in tempo reale
title: Aggiunta di registrazioni e debugging in tempo reale
uuid: 037daf57-a1b3-4b42-ac51-81179fb36915
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Aggiunta di registrazioni e debugging in tempo reale{#add-real-time-logging-and-debugging}

Potete utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.

Il sistema di notifica consente di raccogliere informazioni di registrazione e debug per la diagnostica e la convalida senza che il sistema venga eccessivamente stressato.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non deve gestire il traffico a carico elevato. Se non è necessario che l&#39;implementazione sia completa, considera l&#39;efficienza della trasmissione dei dati per evitare il sovraccarico del sistema.

Di seguito è riportato un esempio di come recuperare le notifiche.

1. Create un thread di esecuzione basato su timer per l’applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.

1. Se l&#39;intervallo del timer è troppo grande e le dimensioni dell&#39;elenco eventi sono troppo piccole, l&#39;elenco degli eventi di notifica si estenda. Per evitare questo overflow, effettuare una delle seguenti operazioni:

   * Diminuisce l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   * Aumentate la dimensione dell&#39;elenco delle notifiche.

1. Serializzare le voci dell&#39;evento di notifica più recente in formato JSON e inviare le voci a un server remoto per la post-elaborazione.

   Il server remoto potrebbe quindi visualizzare graficamente i dati forniti in tempo reale.
1. Per rilevare la perdita di eventi di notifica, cercate gli spazi vuoti nella sequenza di valori di indice dell&#39;evento.

   Ogni evento di notifica ha un valore di indice che viene incrementato automaticamente dalla `session.NotificationHistory` classe.
