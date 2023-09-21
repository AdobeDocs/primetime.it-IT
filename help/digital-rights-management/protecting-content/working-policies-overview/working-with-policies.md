---
title: Panoramica sull'utilizzo dei criteri DRM
description: Panoramica sull'utilizzo dei criteri DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Panoramica {#working-with-drm-policies-overview}

I provider di contenuti possono applicare i criteri DRM ai file multimediali utilizzando l’SDK DRM di Primetime. Gli amministratori possono quindi creare, visualizzare i dettagli e aggiornare i criteri DRM utilizzando le API di gestione dei criteri.

A *`DRM policy`* è una raccolta di informazioni che include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Il criterio definisce il modo in cui gli utenti possono visualizzare il contenuto. Le regole DRM, la crittografia e la firma consentono ai provider di contenuto di mantenere il controllo dei contenuti, indipendentemente dalla loro distribuzione.

Un criterio DRM funge da modello utilizzato dal server licenze per generare una licenza. Un client può anche fare riferimento al criterio DRM prima di richiedere una licenza, per determinare se deve richiedere l&#39;autenticazione all&#39;utente prima di inviare una richiesta di licenza al server.

Puoi distribuire contenuti protetti utilizzando Adobe Flash Media Server o un server HTTP. Gli utenti possono scaricare e riprodurre contenuti protetti in lettori personalizzati generati con l’SDK di Primetime DRM.

Un criterio DRM specifica uno o più diritti concessi al client. In genere, una regola DRM include almeno *`Play Right`*. È inoltre possibile specificare più diritti di riproduzione, ciascuno con restrizioni diverse. Quando il client riceve una licenza con più diritti di riproduzione, utilizza la prima licenza che soddisfa tutte le restrizioni. Ad esempio, puoi applicare impostazioni di protezione dell’output diverse su piattaforme diverse.

Consulta `CreatePolicyWithOutputProtection.java` negli strumenti della riga di comando per l’implementazione di riferimento [!DNL samples] per il codice di esempio che illustra questo esempio.

È possibile completare le seguenti attività con le API di gestione dei criteri DRM di Primetime:

* Creare e aggiornare i criteri
* Visualizza dettagli criteri DRM
* Gestire gli elenchi di aggiornamento dei criteri DRM

Consulta la *Riferimento API di Primetime DRM* per informazioni dettagliate sull’API Java.

Consulta la *Utilizzo delle implementazioni di riferimento DRM di Primetime* per informazioni su Primetime DRM Policy Manager.
