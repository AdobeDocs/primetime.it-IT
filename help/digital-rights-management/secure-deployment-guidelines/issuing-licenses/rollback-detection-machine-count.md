---
description: Se le regole business richiedono la registrazione del numero di computer per un utente, il server licenze o il server di dominio deve memorizzare gli ID computer associati all'utente.
title: Conteggio computer al momento del rilascio delle licenze
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Conteggio computer al momento del rilascio delle licenze {#machine-count-when-issuing-licenses}

Se le regole business richiedono la registrazione del numero di computer per un utente, il server licenze o il server di dominio deve memorizzare gli ID computer associati all&#39;utente.

Il modo più affidabile per tenere traccia degli ID macchina è memorizzare il valore restituito dalla [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) in un database. Quando viene ricevuta una nuova richiesta, confronta l’ID computer nella richiesta con gli ID computer noti utilizzando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) esegue un confronto tra gli ID per determinare se questi rappresentano la stessa macchina. Questo confronto è utile solo se il numero di ID computer è limitato. Ad esempio, se nel dominio degli utenti sono consentiti cinque computer, è possibile cercare nel database gli ID computer associati al nome utente dell&#39;utente e ottenere un piccolo set di dati da confrontare.

Questo confronto non è pratico per le distribuzioni che consentono l’accesso anonimo. In questo caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) possono essere utilizzati. Tuttavia, questo ID non può essere lo stesso se l’utente accede al contenuto dal Flash e dai runtime di Adobe AIR®.

>[!NOTE]
>
>L&#39;ID non viene mantenuto se l&#39;utente riformatta il disco rigido.