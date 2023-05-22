---
title: Utilizzo degli elenchi di aggiornamento dei criteri DRM
description: Utilizzo degli elenchi di aggiornamento dei criteri DRM
copied-description: true
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Elenchi di aggiornamento criteri DRM {#drm-policy-update-lists}

Se si aggiornano le regole di utilizzo in un criterio DRM dopo aver creato un pacchetto di qualsiasi contenuto, è necessario che il server licenze disponga della versione più recente prima di poter rilasciare licenze che utilizzano un criterio DRM aggiornato. Un modo per ottenere questo risultato è tramite un elenco di aggiornamento dei criteri DRM.

Un elenco di aggiornamenti dei criteri DRM è rappresentato da un file che include un elenco di criteri DRM aggiornati o revocati. Ogni volta che si aggiorna un criterio DRM, è necessario generare un nuovo elenco di aggiornamento dei criteri DRM e inviare periodicamente l&#39;elenco a tutti i server licenze.

## Utilizzo degli elenchi di aggiornamento dei criteri DRM {#working-with-drm-policy-update-lists}

Per i server licenze che non hanno accesso a un database per l&#39;archiviazione delle informazioni sui criteri DRM, è possibile utilizzare un elenco di aggiornamento dei criteri DRM per notificare al server licenze eventuali criteri DRM aggiornati. Gli elenchi di aggiornamento dei criteri DRM possono includere versioni aggiornate dei criteri DRM o un elenco di ID dei criteri DRM revocati. Se un elenco di aggiornamento dei criteri è incluso in `HandlerConfiguration`, l’SDK applica questo elenco quando rilascia una licenza.

È inoltre possibile revocare eventuali criteri DRM se i proprietari o i distributori di contenuti desiderano interrompere il rilascio di licenze in base a un determinato criterio DRM. È possibile utilizzare un elenco di aggiornamento dei criteri DRM per applicare la revoca dei criteri DRM nell&#39;SDK. È inoltre possibile applicare gli elenchi di aggiornamento dei criteri DRM per fornire un elenco dei criteri DRM aggiornati all&#39;SDK.

>[!NOTE]
>
>Ogni volta che si revoca una policy DRM, le licenze già rilasciate non vengono revocate automaticamente. Esso impedisce unicamente il rilascio di licenze aggiuntive in base a tale politica DRM.

## Aggiorna elenchi di aggiornamento criteri{#update-policy-update-lists}

L&#39;utilizzo degli elenchi di aggiornamento dei criteri DRM comporta l&#39;utilizzo di un `PolicyUpdateListFactory` oggetto. Se si desidera creare un elenco di aggiornamento dei criteri DRM, è necessario caricare un elenco di aggiornamento dei criteri DRM esistente e quindi verificare se un criterio DRM è stato aggiornato o revocato utilizzando l&#39;API Java.

Per utilizzare gli elenchi di aggiornamento dei criteri DRM:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR inclusi durante la configurazione dell’ambiente di sviluppo in un progetto.
1. Creare un `ServerCredentialFactory` per caricare le credenziali necessarie per la firma.
1. Creare un `PolicyUpdateListFactory` utilizzando il `ServerCredential` che hai creato.
1. Specificare l&#39;ID del criterio DRM da revocare.
1. Creare un `PolicyRevocationEntry` utilizzando l&#39;ID criterio DRM `String` creato e quindi aggiungerlo all&#39;elenco di aggiornamento dei criteri DRM trasmettendolo in `PolicyUpdateListFactory.addRevocationEntry()`.
1. Generare il nuovo elenco di aggiornamento dei criteri DRM chiamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Analogamente, è possibile aggiornare i criteri DRM all&#39;elenco utilizzando `PolicyUpdateEntry`.
1. Se esiste già un elenco di aggiornamento dei criteri DRM, è possibile serializzarlo per il caricamento chiamando `PolicyUpdateList.getBytes()`.

   Per caricare l’elenco, chiama `PolicyUpdateListFactory.loadPolicyUpdateList()` e trasmetterlo nell’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal certificato del server licenze corretto chiamando `PolicyUpdateList.verifySignature()`.
1. Passa l&#39;ID del criterio DRM `String` in `PolicyUpdateList.isRevoked()` per verificare la revoca di una voce.

   In alternativa, puoi passare l’elenco a `HandlerConfiguration` dove viene poi applicata ogni volta che vengono rilasciate licenze.
Se si desidera aggiungere più voci a un `PolicyUpdateList`, è necessario caricare un elenco di aggiornamento dei criteri DRM esistente. Pertanto è necessario creare un nuovo DRM `PolicyUpdateListFactory` dell&#39;istanza. Chiamata `PolicyUpdateListFactory.addEntries` per aggiungere al nuovo elenco tutte le voci del vecchio elenco. Chiamata `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` per aggiungere nuove voci di revoca o aggiornamento a DRM PolicyUpdateList.

Per un codice di esempio che illustra come creare un elenco di aggiornamento dei criteri DRM, vedere `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` nel *Strumenti della riga di comando per l’implementazione di riferimento* [!DNL samples] directory.
