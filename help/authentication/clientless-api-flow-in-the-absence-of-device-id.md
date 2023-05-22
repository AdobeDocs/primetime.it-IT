---
title: Flusso API senza client in assenza di ID dispositivo
description: Flusso API senza client in assenza di ID dispositivo
exl-id: 6549a6d6-03a9-4d95-99fb-d3ada832323d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Flusso API senza client in assenza di ID dispositivo {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>


## Problema

Non tutte le app per Smart Device sono in grado di fornire un ID dispositivo univoco.  Poiché deviceId è un parametro obbligatorio, se non viene passato il servizio restituisce un errore 400.


## Soluzione temporanea/Soluzione alternativa

Per i client senza ID dispositivo:

1. Chiama il servizio del codice di registrazione la prima volta con `deviceId=dummy`
1. Dalla risposta, estrai l’UUID. L’UUID è disponibile nell’elemento &quot;id&quot; della risposta del codice di registrazione (formati di risposta XML e JSON).
1. Richiama il servizio di registrazione una seconda volta. Questa volta, passa `deviceId=<uuid obtained in step #2>`
1. Visualizza il codice di registrazione ottenuto nel passaggio 3 nell’interfaccia utente della console


Al termine di questi passaggi, l’autenticazione Adobe Primetime utilizzerà l’UUID come ID dispositivo. Memorizza questo ID dispositivo (UUID) nell&#39;archivio locale del dispositivo. Nel caso in cui l’utente generi un nuovo codice di registrazione, è necessario eseguire nuovamente i passaggi da 1 a 4 e quindi sostituire l’ID dispositivo (UUID) memorizzato in precedenza con il nuovo.



## Soluzione permanente

L’Adobe cambierà questo in una versione futura, rendendo `deviceId` un payload opzionale durante la creazione del codice reg e utilizzando UUID come chiave del token invece di `deviceId`, quando `deviceId` non è presente.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
