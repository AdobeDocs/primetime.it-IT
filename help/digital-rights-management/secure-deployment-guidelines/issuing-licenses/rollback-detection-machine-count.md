---
description: Se le regole business richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all'utente.
title: Conteggio automatico al momento del rilascio delle licenze
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Numero di macchine al momento del rilascio delle licenze {#machine-count-when-issuing-licenses}

Se le regole business richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all&#39;utente.

Il modo più efficace per tenere traccia degli ID computer è quello di memorizzare il valore restituito dal metodo [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) in un database. Quando viene ricevuta una nuova richiesta, confronta l’ID computer nella richiesta con gli ID computer noti utilizzando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) esegue un confronto degli ID per determinare se gli ID rappresentano la stessa macchina. Questo confronto è pratico solo se è presente un numero limitato di ID macchina. Ad esempio, se agli utenti sono consentiti cinque computer nel loro dominio, puoi cercare nel database gli ID computer associati al nome utente dell’utente e ottenere un piccolo set di dati da confrontare.

Questo confronto non è pratico per le distribuzioni che consentono l’accesso anonimo. In questo caso, è possibile utilizzare [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()). Tuttavia, questo ID non può essere lo stesso se l&#39;utente accede al contenuto dai runtime Flash e Adobe AIR®.

>[!NOTE]
>
>L&#39;ID non sopravvive se l&#39;utente riformatta il disco rigido.