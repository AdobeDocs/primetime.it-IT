---
title: Panoramica sull'utilizzo dei criteri DRM
description: Panoramica sull'utilizzo dei criteri DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Panoramica {#working-with-drm-policies-overview}

I fornitori di contenuti possono applicare criteri DRM ai file multimediali utilizzando l’SDK DRM di Primetime. Gli amministratori possono quindi creare, visualizzare i dettagli e aggiornare i criteri DRM utilizzando le API di gestione dei criteri.

Un *`DRM policy`* è una raccolta di informazioni che include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Il criterio definisce il modo in cui gli utenti possono visualizzare il contenuto. I criteri, la crittografia e la firma DRM consentono ai fornitori di contenuti di mantenere il controllo dei contenuti indipendentemente dalla loro diffusione.

Un criterio DRM funge da modello utilizzato dal server licenze quando genera una licenza. Un client può anche fare riferimento al criterio DRM prima di richiedere una licenza, per determinare se il client deve richiedere l&#39;autenticazione all&#39;utente prima di emettere una richiesta di licenza al server.

È possibile fornire contenuto protetto utilizzando un Flash Media Server di Adobe o un server HTTP. Gli utenti possono scaricare e riprodurre contenuti protetti in lettori personalizzati creati con Primetime DRM SDK.

Un criterio DRM specifica uno o più diritti concessi al client. In genere, un criterio DRM include almeno *`Play Right`*. Puoi anche specificare più diritti di riproduzione, ciascuno con diverse restrizioni. Quando il cliente riceve una licenza con più diritti di riproduzione, utilizza la prima licenza che soddisfa tutte le restrizioni. Ad esempio, puoi applicare diverse impostazioni di protezione dell’output su piattaforme diverse.

Per un esempio di codice che illustra questo esempio, consulta `CreatePolicyWithOutputProtection.java` nella directory Strumenti della riga di comando per l’implementazione di riferimento [!DNL samples] .

Puoi completare le seguenti attività con le API di gestione dei criteri DRM di Primetime:

* Creare e aggiornare i criteri
* Visualizza i dettagli dei criteri DRM
* Gestisci elenchi di aggiornamento dei criteri DRM

Per informazioni dettagliate sull&#39;API Java, consulta *Riferimento API DRM di Primetime* .

Per informazioni su Primetime DRM Policy Manager, consulta la guida *Using the Primetime DRM Reference Implementations* .
