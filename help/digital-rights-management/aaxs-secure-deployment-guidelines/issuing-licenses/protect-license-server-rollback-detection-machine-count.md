---
title: Conteggio automatico al momento del rilascio delle licenze
description: Conteggio automatico al momento del rilascio delle licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Numero di computer al momento del rilascio delle licenze{#machine-count-when-issuing-licenses}

Se le regole business richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all&#39;utente. Il modo più efficace per tenere traccia degli ID macchina è quello di memorizzare il valore restituito dal metodo `MachineId.getBytes()` in un database. Quando arriva una nuova richiesta, confronta l’ID computer della richiesta con gli ID computer noti che utilizzano `MachineId.matches()`.

`MachineId.matches()` esegue un confronto degli ID per determinare se rappresentano la stessa macchina. Questo confronto è pratico solo se è presente un numero limitato di ID computer da confrontare. Ad esempio, se a un utente sono consentiti cinque computer all’interno del proprio dominio, è possibile cercare nel database gli ID computer associati al nome utente dell’utente e ottenere un piccolo set di dati da confrontare.

>[!NOTE]
>
>Questo confronto non è pratico per le distribuzioni che consentono l’accesso anonimo. In questi casi `MachineId.getUniqueID()` può essere utilizzato, tuttavia, questo ID non sarà lo stesso se l&#39;utente accede al contenuto dei runtime sia di Flash che di Adobe AIR® e non sopravviverà se l&#39;utente riformatta il proprio disco rigido.

Per ulteriori informazioni su `MachineToken.getMachineId()`e `MachineId.matches()`, consulta *Riferimento API di accesso Adobe*.
