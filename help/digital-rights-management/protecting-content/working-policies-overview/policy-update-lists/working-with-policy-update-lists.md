---
seo-title: Utilizzo degli elenchi di aggiornamento dei criteri DRM
title: Utilizzo degli elenchi di aggiornamento dei criteri DRM
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Elenchi di aggiornamento criteri DRM {#drm-policy-update-lists}

Se aggiornate le regole di utilizzo in un criterio DRM dopo aver creato il pacchetto di qualsiasi contenuto, il server licenze deve disporre della versione più recente prima di poter rilasciare licenze che utilizzano un criterio DRM aggiornato. Un modo per ottenere questo risultato è tramite un elenco di aggiornamento dei criteri DRM.

Un elenco di aggiornamento dei criteri DRM è rappresentato da un file che include un elenco di criteri DRM aggiornati o revocati. Ogni volta che aggiornate un criterio DRM, dovete generare un nuovo elenco di aggiornamento criteri DRM e inviare periodicamente l&#39;elenco a tutti i server licenze.

## Utilizzo degli elenchi di aggiornamento dei criteri DRM {#working-with-drm-policy-update-lists}

Per i server licenze che non dispongono dell&#39;accesso a un database per la memorizzazione delle informazioni sui criteri DRM, può essere necessario utilizzare un elenco di aggiornamento dei criteri DRM per notificare al server licenze eventuali criteri DRM aggiornati. Gli elenchi degli aggiornamenti dei criteri DRM possono includere versioni aggiornate dei criteri DRM o un elenco degli ID dei criteri DRM revocati. Se un elenco di aggiornamento dei criteri è incluso in `HandlerConfiguration`, l&#39;SDK applica questo elenco quando rilascia una licenza.

È inoltre possibile revocare qualsiasi criterio DRM se i proprietari o i distributori di contenuti desiderano interrompere il rilascio delle licenze in base a una determinata politica DRM. Un elenco di aggiornamento dei criteri DRM può essere utilizzato per applicare la revoca dei criteri DRM nell&#39;SDK. Puoi anche applicare elenchi di aggiornamento criteri DRM per fornire un elenco di criteri DRM aggiornati all&#39;SDK.

>[!NOTE]
>
>Ogni volta che revocate un criterio DRM, tutte le licenze già rilasciate non vengono automaticamente revocate. Impedisce solo il rilascio di licenze aggiuntive in base a tale criterio DRM.

## Aggiorna elenchi aggiornamenti criteri{#update-policy-update-lists}

L&#39;utilizzo degli elenchi di aggiornamento dei criteri DRM implica l&#39;utilizzo di un `PolicyUpdateListFactory` oggetto. Se si desidera creare un elenco di aggiornamento criteri DRM, è necessario caricare un elenco di aggiornamento criteri DRM esistente, quindi verificare se un criterio DRM è stato aggiornato o revocato utilizzando l&#39;API Java.

Per utilizzare gli elenchi di aggiornamento criteri DRM:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR inclusi quando configurate l&#39;ambiente di sviluppo in un progetto.
1. Creare un&#39; `ServerCredentialFactory` istanza per caricare le credenziali necessarie per la firma.
1. Create un’ `PolicyUpdateListFactory` istanza utilizzando l’ `ServerCredential` istanza creata.
1. Specificate l&#39;ID del criterio DRM da revocare.
1. Create un `PolicyRevocationEntry` oggetto utilizzando l&#39;ID del criterio DRM `String` appena creato, quindi aggiungetelo all&#39;elenco di aggiornamento del criterio DRM trasmettendolo in `PolicyUpdateListFactory.addRevocationEntry()`.
1. Generate il nuovo elenco di aggiornamento dei criteri DRM chiamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Allo stesso modo, potete aggiornare i criteri DRM all&#39;elenco utilizzando `PolicyUpdateEntry`.
1. Se esiste già un elenco di aggiornamento criteri DRM, puoi serializzarlo per il caricamento chiamando `PolicyUpdateList.getBytes()`.

   Per caricare l’elenco, chiamarlo `PolicyUpdateListFactory.loadPolicyUpdateList()` e trasmetterlo nell’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal certificato corretto del server licenze chiamando `PolicyUpdateList.verifySignature()`.
1. Passa l&#39;ID del criterio DRM `String` in `PolicyUpdateList.isRevoked()` per verificare che una voce sia stata revocata.

   In alternativa, è possibile trasmettere l&#39;elenco alla `HandlerConfiguration` posizione in cui viene applicata ogni volta che vengono rilasciate le licenze.
Se si desidera aggiungere altre voci a un elenco esistente `PolicyUpdateList`, è necessario caricare un elenco esistente di aggiornamento dei criteri DRM. È pertanto necessario creare una nuova `PolicyUpdateListFactory` istanza DRM. Chiamata `PolicyUpdateListFactory.addEntries` per aggiungere tutte le voci dal vecchio elenco al nuovo elenco. Chiamare `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` aggiungere nuove voci di revoca o aggiornamento a DRM PolicyUpdateList.

Per un esempio di codice che illustra come creare un elenco di aggiornamento dei criteri DRM, vedere `com.adobe.flashaccess.samples.policyupdatelist` nella directory Strumenti `.CreatePolicyUpdateList` della riga di comando della riga di comando Implementazione di *riferimento* [!DNL samples] .
