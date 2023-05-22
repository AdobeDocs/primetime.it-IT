---
title: Utilizzo degli elenchi di aggiornamento dei criteri
description: Utilizzo degli elenchi di aggiornamento dei criteri
copied-description: true
exl-id: 71715eec-e6a3-4640-b17f-ec0c38caf73e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Utilizzo degli elenchi di aggiornamento dei criteri{#working-with-policy-update-lists}

Per i server licenze che non hanno accesso a un database per l&#39;archiviazione di informazioni sui criteri, è possibile utilizzare un elenco di aggiornamento dei criteri per notificare i criteri aggiornati al server licenze. Gli elenchi di aggiornamento dei criteri possono contenere versioni aggiornate dei criteri o un elenco di ID dei criteri revocati. Se in viene fornito un elenco di aggiornamento dei criteri `HandlerConfiguration`, l’SDK applicherà questo elenco quando si rilascia una licenza.

I criteri possono anche essere revocati se i proprietari o i distributori di contenuti desiderano interrompere il rilascio delle licenze in base a un determinato criterio. È possibile utilizzare un elenco di aggiornamento dei criteri per applicare la revoca dei criteri nell’SDK. Gli elenchi di aggiornamento dei criteri possono essere utilizzati anche per fornire un elenco di criteri aggiornati all’SDK. La revoca di un criterio non comporta la revoca delle licenze già rilasciate. Esso impedisce soltanto il rilascio di licenze aggiuntive in base a tale politica.

L’utilizzo degli elenchi di aggiornamento dei criteri comporta l’utilizzo di un’ `PolicyUpdateListFactory` oggetto. Per creare un elenco di aggiornamento dei criteri, caricare un elenco di aggiornamento dei criteri esistente e verificare se un criterio è stato aggiornato o revocato utilizzando l’API Java, attenersi alla procedura descritta di seguito.

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in Configurazione dell’ambiente di sviluppo all’interno del progetto.
1. Creare un `ServerCredentialFactory` per caricare le credenziali necessarie per la firma.
1. Creare un `PolicyUpdateListFactory` istanza che utilizza `ServerCredential` hai creato.
1. Specifica l’ID del criterio da revocare.
1. Creare un `PolicyRevocationEntry` oggetto utilizzando l’ID della policy `String` hai appena creato e lo aggiungi all’elenco di aggiornamento dei criteri trasmettendolo in `PolicyUpdateListFactory.addRevocationEntry()`. Genera il nuovo elenco di aggiornamenti dei criteri chiamando `PolicyUpdateListFactory.generatePolicyUpdateList()`. Allo stesso modo, è possibile aggiungere criteri aggiornati all’elenco utilizzando `PolicyUpdateEntry`.
1. Se esiste già un elenco di aggiornamento dei criteri, è possibile serializzarlo per il caricamento chiamando `PolicyUpdateList.getBytes()`. Per caricare l’elenco, chiama `PolicyUpdateListFactory.loadPolicyUpdateList()` e passa nell’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal certificato del server licenze corretto chiamando `PolicyUpdateList.verifySignature()`.
1. Per verificare se una voce è stata revocata, passa l’ID del criterio `String` in `PolicyUpdateList.isRevoked()`. In alternativa, è possibile passare l’elenco in `HandlerConfiguration` e verrà applicato al momento del rilascio delle licenze.

Per aggiungere altre voci a un elemento esistente `PolicyUpdateList`, carica un elenco di aggiornamento dei criteri esistente. Crea un nuovo `PolicyUpdateListFactory` dell&#39;istanza. Chiama P `olicyUpdateListFactory.addEntries` per aggiungere al nuovo elenco tutte le voci del vecchio elenco. Chiamata `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` per aggiungere nuove voci di revoca o aggiornamento a PolicyUpdateList.

Per un codice di esempio che illustra come creare un elenco di aggiornamento dei criteri, caricare un elenco di aggiornamento dei criteri esistente e verificare se un criterio è stato revocato, vedere `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
