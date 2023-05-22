---
title: Conteggio computer al momento del rilascio delle licenze
description: Conteggio computer al momento del rilascio delle licenze
copied-description: true
exl-id: de052e98-8ae3-4e12-8f77-787293edda39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Conteggio computer al momento del rilascio delle licenze{#machine-count-when-issuing-licenses}

Se le regole business richiedono la registrazione del numero di computer per un utente, il server licenze o il server di dominio deve memorizzare gli ID computer associati all&#39;utente. Il modo più affidabile per tenere traccia degli ID macchina è memorizzare il valore restituito dalla `MachineId.getBytes()` in un database. Quando arriva una nuova richiesta, confronta l’ID computer nella richiesta con gli ID computer noti utilizzando `MachineId.matches()`.

`MachineId.matches()` esegue un confronto tra gli ID per determinare se rappresentano la stessa macchina. Questo confronto è utile solo se è presente un numero limitato di ID computer da confrontare. Ad esempio, se a un utente sono consentiti cinque computer all’interno del proprio dominio, puoi cercare nel database gli ID computer associati al nome utente dell’utente e ottenere un piccolo set di dati con cui confrontare il dato.

>[!NOTE]
>
>Questo confronto non è pratico per le distribuzioni che consentono l’accesso anonimo. In tali casi `MachineId.getUniqueID()` può essere utilizzato, tuttavia, questo ID non sarà lo stesso se l&#39;utente accede al contenuto sia dal Flash che da Adobe AIR® runtime e non sopravvivrà se l&#39;utente riformatta il proprio disco rigido.

Per ulteriori informazioni su `MachineToken.getMachineId()`e `MachineId.matches()`, vedere *Riferimento API per l’accesso agli Adobi*.
