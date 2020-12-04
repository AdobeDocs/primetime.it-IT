---
seo-title: Conteggio computer al momento del rilascio delle licenze
title: Conteggio computer al momento del rilascio delle licenze
uuid: d57f8b0b-0363-4b26-bd71-76f4abe5b68f
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Conteggio computer per il rilascio delle licenze{#machine-count-when-issuing-licenses}

Se le regole aziendali richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all&#39;utente. Il modo più efficace per tenere traccia degli ID computer è quello di memorizzare il valore restituito dal metodo `MachineId.getBytes()` in un database. Quando arriva una nuova richiesta, confrontate l&#39;ID computer della richiesta con gli ID computer noti utilizzando `MachineId.matches()`.

`MachineId.matches()` esegue un confronto degli ID per determinare se rappresentano lo stesso computer. Questo confronto è pratico solo se è presente un numero limitato di ID computer da confrontare. Ad esempio, se a un utente sono consentite cinque computer all&#39;interno del loro dominio, è possibile ricercare nel database gli ID computer associati al nome utente dell&#39;utente e ottenere un piccolo set di dati da confrontare.

>[!NOTE]
>
>Questo confronto non è pratico per le installazioni che consentono l&#39;accesso anonimo. In tali casi `MachineId.getUniqueID()` può essere utilizzato, tuttavia, questo ID non sarà lo stesso se l&#39;utente accede al contenuto sia dai runtime Adobe AIR® che  Flash, e non sopravviverà se l&#39;utente riformatta il disco rigido.

Per ulteriori informazioni su `MachineToken.getMachineId()`e `MachineId.matches()`, vedere la *Guida di riferimento API per l&#39;accesso ai Adobi*.
