---
title: Utilizzo degli elenchi di aggiornamento dei criteri
description: Utilizzo degli elenchi di aggiornamento dei criteri
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Utilizzo degli elenchi di aggiornamento dei criteri{#working-with-policy-update-lists}

Per i server licenze che non hanno accesso a un database per la memorizzazione di informazioni sui criteri, è possibile utilizzare un elenco di aggiornamento dei criteri per notificare al server licenze i criteri aggiornati. Gli elenchi degli aggiornamenti dei criteri possono contenere versioni aggiornate dei criteri o un elenco di ID dei criteri revocati. Se in `HandlerConfiguration` viene fornito un elenco di aggiornamenti dei criteri, l&#39;SDK applicherà questo elenco al momento del rilascio di una licenza.

Le politiche possono anche essere revocate se i proprietari o i distributori di contenuti desiderano interrompere il rilascio delle licenze in base a una particolare politica. Un elenco di aggiornamento dei criteri può essere utilizzato per applicare la revoca dei criteri nell&#39;SDK. Gli elenchi di aggiornamento dei criteri possono anche essere utilizzati per fornire un elenco dei criteri aggiornati all&#39;SDK. La revoca di un criterio non revoca le licenze già rilasciate. Essa impedisce soltanto il rilascio di ulteriori licenze nell&#39;ambito di tale politica.

L&#39;utilizzo degli elenchi di aggiornamento dei criteri comporta l&#39;utilizzo di un oggetto `PolicyUpdateListFactory`. Per creare un elenco di aggiornamento dei criteri, caricare un elenco di aggiornamento dei criteri esistente e verificare se un criterio è stato aggiornato o revocato utilizzando l&#39;API Java, esegui le seguenti operazioni:

1. Imposta l’ambiente di sviluppo e includi tutti i file JAR menzionati in Impostazione dell’ambiente di sviluppo all’interno del progetto.
1. Crea un&#39;istanza `ServerCredentialFactory` per caricare le credenziali necessarie per la firma.
1. Crea un&#39;istanza `PolicyUpdateListFactory` utilizzando il `ServerCredential` creato.
1. Specifica l&#39;ID del criterio da revocare.
1. Crea un oggetto `PolicyRevocationEntry` utilizzando l&#39;ID criterio `String` appena creato e aggiungilo all&#39;elenco di aggiornamento dei criteri trasmettendolo in `PolicyUpdateListFactory.addRevocationEntry()`. Genera il nuovo elenco di aggiornamenti dei criteri chiamando `PolicyUpdateListFactory.generatePolicyUpdateList()`. Allo stesso modo, è possibile aggiungere all’elenco criteri aggiornati utilizzando `PolicyUpdateEntry`.
1. Se esiste già un elenco di aggiornamento dei criteri, puoi serializzarlo per il caricamento chiamando `PolicyUpdateList.getBytes()`. Per caricare l’elenco, chiama `PolicyUpdateListFactory.loadPolicyUpdateList()` e passa l’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal certificato corretto del server di licenze chiamando `PolicyUpdateList.verifySignature()`.
1. Per verificare se una voce è stata revocata, passa l&#39;ID criterio `String` in `PolicyUpdateList.isRevoked()`. In alternativa, l’elenco può essere trasmesso in `HandlerConfiguration` e verrà applicato al momento del rilascio delle licenze.

Per aggiungere altre voci a un `PolicyUpdateList` esistente, carica un elenco di aggiornamento dei criteri esistente. Crea una nuova istanza `PolicyUpdateListFactory`. Invoca P `olicyUpdateListFactory.addEntries` per aggiungere tutte le voci del vecchio elenco al nuovo elenco. Chiamare `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` per aggiungere nuove voci di revoca o aggiornamento a PolicyUpdateList.

Per un esempio di codice che illustra come creare un elenco di aggiornamenti dei criteri, caricare un elenco di aggiornamenti dei criteri esistenti e verificare se un criterio è stato revocato, vedere `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
