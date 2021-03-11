---
title: Utilizzo degli elenchi di aggiornamento dei criteri DRM
description: Utilizzo degli elenchi di aggiornamento dei criteri DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Elenchi di aggiornamento dei criteri DRM {#drm-policy-update-lists}

Se si aggiornano le regole di utilizzo in un criterio DRM dopo aver compilato un contenuto, il server licenze deve disporre della versione più recente prima di poter rilasciare licenze che utilizzano un criterio DRM aggiornato. Un modo per ottenere questo risultato è tramite un elenco di aggiornamento dei criteri DRM.

Un elenco di aggiornamento dei criteri DRM è rappresentato da un file che include un elenco di criteri DRM aggiornati o revocati. Ogni volta che aggiorni un criterio DRM, devi generare un nuovo elenco di aggiornamento dei criteri DRM e inviare periodicamente l’elenco a tutti i server di licenza.

## Utilizzo degli elenchi di aggiornamento dei criteri DRM {#working-with-drm-policy-update-lists}

Per i server licenze che non hanno accesso a un database per la memorizzazione di informazioni sui criteri DRM, può essere utile utilizzare un elenco di aggiornamento dei criteri DRM per notificare al server licenze eventuali criteri DRM aggiornati. Gli elenchi di aggiornamento dei criteri DRM possono includere versioni aggiornate dei criteri DRM o un elenco di ID dei criteri DRM revocati. Se in `HandlerConfiguration` è incluso un elenco di aggiornamento dei criteri, l&#39;SDK lo applica quando rilascia una licenza.

È inoltre possibile revocare qualsiasi politica DRM se i proprietari o i distributori di contenuti desiderano interrompere il rilascio delle licenze in base a una particolare politica DRM. Un elenco di aggiornamento dei criteri DRM può essere utilizzato per applicare la revoca dei criteri DRM nell&#39;SDK. Puoi anche applicare gli elenchi di aggiornamento dei criteri DRM per fornire all’SDK un elenco di criteri DRM aggiornati.

>[!NOTE]
>
>Ogni volta che revochi una politica DRM, tutte le licenze già rilasciate non vengono automaticamente revocate. Impedisce solo il rilascio di licenze supplementari in base a tale politica DRM.

## Aggiorna elenchi di aggiornamento dei criteri{#update-policy-update-lists}

L’utilizzo degli elenchi di aggiornamento dei criteri DRM comporta l’utilizzo di un oggetto `PolicyUpdateListFactory`. Se desideri creare un elenco di aggiornamento dei criteri DRM, devi caricare un elenco esistente di aggiornamento dei criteri DRM, quindi verificare se un criterio DRM è stato aggiornato o revocato utilizzando l&#39;API Java.

Per utilizzare gli elenchi di aggiornamento dei criteri DRM:

1. Imposta l’ambiente di sviluppo e includi tutti i file JAR inclusi quando configuri l’ambiente di sviluppo in un progetto .
1. Creare un&#39;istanza `ServerCredentialFactory` per caricare le credenziali necessarie per la firma.
1. Crea un&#39;istanza `PolicyUpdateListFactory` utilizzando il `ServerCredential` creato.
1. Specifica l’ID del criterio DRM da revocare.
1. Crea un oggetto `PolicyRevocationEntry` utilizzando l&#39;ID criterio DRM `String` appena creato, quindi aggiungilo all&#39;elenco di aggiornamento dei criteri DRM trasmettendolo in `PolicyUpdateListFactory.addRevocationEntry()`.
1. Genera il nuovo elenco di aggiornamento dei criteri DRM chiamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Allo stesso modo, è possibile aggiornare i criteri DRM all&#39;elenco utilizzando `PolicyUpdateEntry`.
1. Se esiste già un elenco di aggiornamento dei criteri DRM, puoi serializzarlo per il caricamento chiamando `PolicyUpdateList.getBytes()`.

   Per caricare l’elenco, invoca `PolicyUpdateListFactory.loadPolicyUpdateList()` e trasmettilo nell’elenco serializzato.
1. Verifica che la firma sia valida e che l’elenco sia stato firmato dal certificato corretto del server di licenze chiamando `PolicyUpdateList.verifySignature()`.
1. Passa l’ID del criterio DRM `String` in `PolicyUpdateList.isRevoked()` per verificare che una voce sia stata revocata.

   In alternativa, è possibile passare l’elenco a `HandlerConfiguration` dove viene applicato ogni volta che vengono rilasciate le licenze.
Se desideri aggiungere più voci a un `PolicyUpdateList` esistente, devi caricare un elenco di aggiornamento dei criteri DRM esistente. Pertanto devi creare una nuova istanza DRM `PolicyUpdateListFactory`. Invoca `PolicyUpdateListFactory.addEntries` per aggiungere tutte le voci del vecchio elenco al nuovo elenco. Chiamare `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` per aggiungere nuove voci di revoca o aggiornamento al DRM PolicyUpdateList.

Per un esempio di codice che illustra come creare un elenco di aggiornamenti dei criteri DRM, consulta `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` nella directory *Strumenti della riga di comando per l’implementazione di riferimento* [!DNL samples] .
