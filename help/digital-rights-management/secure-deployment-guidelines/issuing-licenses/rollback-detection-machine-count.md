---
description: Se le regole aziendali richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all'utente.
seo-description: Se le regole aziendali richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all'utente.
seo-title: Conteggio computer al momento del rilascio delle licenze
title: Conteggio computer al momento del rilascio delle licenze
uuid: 7ba8a8d4-a31f-4f37-82a7-755cfa443544
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Conteggio computer per il rilascio delle licenze {#machine-count-when-issuing-licenses}

Se le regole aziendali richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all&#39;utente.

Il modo più efficace per tenere traccia degli ID computer è quello di memorizzare il valore restituito dal metodo [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) in un database. Quando viene ricevuta una nuova richiesta, confrontate l&#39;ID computer della richiesta con gli ID computer noti utilizzando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches() ](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) esegue un confronto degli ID per determinare se gli ID rappresentano lo stesso computer. Questo confronto è pratico solo se è presente un numero limitato di ID computer. Ad esempio, se agli utenti sono concessi cinque computer nel loro dominio, è possibile ricercare nel database gli ID computer associati al nome utente dell&#39;utente e ottenere un piccolo set di dati per il confronto.

Questo confronto non è pratico per le installazioni che consentono l&#39;accesso anonimo. In questo caso, è possibile utilizzare [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()). Tuttavia, questo ID non può essere lo stesso se l&#39;utente accede al contenuto dai runtime Adobe AIR® e di Flash e .

>[!NOTE]
>
>L&#39;ID non sopravvive se l&#39;utente riformatta il disco rigido.