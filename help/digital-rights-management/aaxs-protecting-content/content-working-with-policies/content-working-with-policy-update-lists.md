---
seo-title: Utilizzo degli elenchi di aggiornamento dei criteri
title: Utilizzo degli elenchi di aggiornamento dei criteri
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Utilizzo degli elenchi di aggiornamento dei criteri{#working-with-policy-update-lists}

Per i server di licenze che non dispongono dell&#39;accesso a un database per la memorizzazione delle informazioni sui criteri, è possibile utilizzare un elenco di aggiornamento dei criteri per notificare al server licenze i criteri aggiornati. Gli elenchi degli aggiornamenti dei criteri possono contenere versioni aggiornate dei criteri o un elenco di ID di criteri revocati. Se viene fornito un elenco di aggiornamento dei criteri in `HandlerConfiguration`, l&#39;SDK applicherà questo elenco al momento dell&#39;emissione di una licenza.

Le politiche possono anche essere revocate se i proprietari o i distributori di contenuti intendono interrompere il rilascio delle licenze in base a una determinata politica. Un elenco di aggiornamento dei criteri può essere utilizzato per applicare la revoca dei criteri nell&#39;SDK. Gli elenchi degli aggiornamenti dei criteri possono essere utilizzati anche per fornire un elenco dei criteri aggiornati all&#39;SDK. La revoca di un criterio non revoca le licenze già rilasciate. Impedisce solo il rilascio di licenze supplementari in base a tale politica.

L&#39;utilizzo degli elenchi di aggiornamento dei criteri implica l&#39;utilizzo di un `PolicyUpdateListFactory` oggetto. Per creare un elenco di aggiornamento dei criteri, caricare un elenco di aggiornamento dei criteri esistente e verificare se un criterio è stato aggiornato o revocato utilizzando l&#39;API Java, eseguire le operazioni seguenti:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR citati in Impostazione dell&#39;ambiente di sviluppo all&#39;interno del progetto.
1. Creare un&#39; `ServerCredentialFactory` istanza per caricare le credenziali necessarie per la firma.
1. Create un’ `PolicyUpdateListFactory` istanza utilizzando l’ `ServerCredential` elemento creato.
1. Specificate l&#39;ID del criterio da revocare.
1. Create un `PolicyRevocationEntry` oggetto utilizzando l&#39;ID del criterio `String` appena creato e aggiungetelo all&#39;elenco di aggiornamento del criterio trasmettendolo in `PolicyUpdateListFactory.addRevocationEntry()`. Generate il nuovo elenco di aggiornamento dei criteri chiamando `PolicyUpdateListFactory.generatePolicyUpdateList()`. Allo stesso modo, è possibile aggiungere criteri aggiornati all&#39;elenco utilizzando `PolicyUpdateEntry`.
1. Se esiste già un elenco di aggiornamento dei criteri, potete serializzarlo per il caricamento chiamando `PolicyUpdateList.getBytes()`. Per caricare l’elenco, chiamare `PolicyUpdateListFactory.loadPolicyUpdateList()` e trasmettere l’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal certificato del server licenze corretto chiamando `PolicyUpdateList.verifySignature()`.
1. Per verificare se una voce è stata revocata, trasmettete l&#39;ID del criterio `String` in `PolicyUpdateList.isRevoked()`. In alternativa, l&#39;elenco può essere trasmesso `HandlerConfiguration` e verrà applicato al momento del rilascio delle licenze.

Per aggiungere altre voci a un elenco esistente `PolicyUpdateList`, caricate un elenco di aggiornamento dei criteri esistente. Create una nuova `PolicyUpdateListFactory` istanza. Chiama P `olicyUpdateListFactory.addEntries` per aggiungere tutte le voci dal vecchio elenco al nuovo elenco. Chiamare `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` aggiungere nuove voci di revoca o aggiornamento a PolicyUpdateList.

Per un esempio di codice che illustra come creare un elenco di aggiornamento dei criteri, caricare un elenco di aggiornamento dei criteri esistente e verificare se un criterio è stato revocato, vedere `com.adobe.flashaccess.samples.policyupdatelist` nella directory &quot;sample&quot; degli strumenti della riga di comando di implementazione di riferimento `.CreatePolicyUpdateList` nella directory &quot;samples&quot; degli strumenti della riga di comando.
