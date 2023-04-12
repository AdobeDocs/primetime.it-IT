---
title: Flusso API senza client in assenza di ID dispositivo
description: Flusso API senza client in assenza di ID dispositivo
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Flusso API senza client in assenza di ID dispositivo {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>


## Problema

Non tutte le app per dispositivi avanzati saranno in grado di fornire un ID dispositivo univoco.  Dato che deviceId è un parametro obbligatorio, il servizio restituisce un errore 400 se non viene passato.


## Soluzione temporanea / Soluzione alternativa

Per i client privi di ID dispositivo:

1. Chiama il servizio del codice di registrazione la prima volta con `deviceId=dummy`
1. Dalla risposta, estrai l’UUID. L’UUID è disponibile nell’elemento &quot;id&quot; della risposta al codice di registrazione (formati di risposta XML e JSON).
1. Chiama il servizio di registrazione una seconda volta. Questa volta, passa `deviceId=<uuid obtained in step #2>`
1. Visualizza il codice di registrazione ottenuto al passaggio 3 nell’interfaccia utente della console


Al termine di questi passaggi, l’autenticazione Adobe Primetime utilizzerà l’UUID come ID dispositivo. Memorizza questo ID dispositivo (UUID) nell&#39;archivio locale del dispositivo. Nel caso in cui l&#39;utente generi un nuovo codice di registrazione, esegui di nuovo i passaggi da 1 a 4 e sostituisci l&#39;ID dispositivo (UUID) precedentemente memorizzato con il nuovo.



## Soluzione permanente

Adobe modificherà questa impostazione in una versione futura, effettuando le seguenti operazioni `deviceId` un payload facoltativo durante la creazione del codice reg e l’utilizzo di UUID come chiave token invece di `deviceId`quando `deviceId` non è presente.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->