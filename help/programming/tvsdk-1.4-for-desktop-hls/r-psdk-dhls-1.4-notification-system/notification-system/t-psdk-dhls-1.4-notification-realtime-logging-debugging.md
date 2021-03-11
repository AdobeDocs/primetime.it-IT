---
description: Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nella tua applicazione video.
title: Aggiungere registrazione e debug in tempo reale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Aggiungi registrazione e debug in tempo reale{#add-real-time-logging-and-debugging}

Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nella tua applicazione video.

Il sistema di notifica ti consente di raccogliere informazioni di registrazione e debug per scopi diagnostici e di convalida senza che il sistema venga eccessivamente stressato.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non deve gestire il traffico ad alto carico. Se l’implementazione non deve essere completa, considera l’efficienza della trasmissione dei dati per evitare di sovraccaricare il sistema.

Ecco un esempio di come recuperare le notifiche.

1. Crea un thread di esecuzione basato su timer per l&#39;applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.

1. Se l&#39;intervallo del timer è troppo grande e le dimensioni dell&#39;elenco degli eventi sono troppo piccole, l&#39;elenco degli eventi di notifica si sovrapporrà. Per evitare questo overflow, effettuare una delle seguenti operazioni:

   * Diminuisce l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   * Aumenta le dimensioni dell’elenco delle notifiche.

1. Serializza le voci dell&#39;evento di notifica più recenti in formato JSON e invia le voci a un server remoto per la post-elaborazione.

   Il server remoto potrebbe quindi visualizzare graficamente i dati forniti in tempo reale.
1. Per rilevare la perdita degli eventi di notifica, cerca le lacune nella sequenza di valori di indice degli eventi.

   Ogni evento di notifica ha un valore di indice che viene incrementato automaticamente dalla classe `NotificationHistory`.
