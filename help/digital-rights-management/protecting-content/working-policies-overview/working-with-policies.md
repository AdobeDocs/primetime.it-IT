---
seo-title: Panoramica sull'utilizzo dei criteri DRM
title: Panoramica sull'utilizzo dei criteri DRM
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Panoramica {#working-with-drm-policies-overview}

I fornitori di contenuti possono applicare criteri DRM ai file multimediali utilizzando l&#39;SDK DRM di Primetime. Gli amministratori possono quindi creare, visualizzare i dettagli e aggiornare i criteri DRM utilizzando le API di gestione dei criteri.

Un *`DRM policy`* è una raccolta di informazioni che include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Il criterio definisce il modo in cui gli utenti possono visualizzare il contenuto. I criteri DRM, la cifratura e la firma consentono ai fornitori di contenuti di mantenere il controllo dei contenuti indipendentemente dalla loro ampiezza di distribuzione.

Un criterio DRM funge da modello utilizzato dal server licenze per generare una licenza. Un client può anche fare riferimento al criterio DRM prima di richiedere una licenza, per determinare se il client deve richiedere all&#39;utente l&#39;autenticazione prima di inviare una richiesta di licenza al server.

Potete fornire contenuto protetto tramite  Flash Media Server di Adobe o un server HTTP. Gli utenti possono scaricare e riprodurre contenuto protetto in lettori personalizzati creati con Primetime DRM SDK.

Un criterio DRM specifica uno o più diritti concessi al client. In genere, un criterio DRM include, come minimo, la variabile *`Play Right`*. Potete anche specificare più diritti di riproduzione, ciascuno con diverse limitazioni. Quando il cliente riceve una licenza con più diritti di riproduzione, utilizza la prima licenza che soddisfa tutte le restrizioni. Ad esempio, è possibile applicare diverse impostazioni di protezione dell&#39;output su piattaforme diverse.

Per un esempio di codice che illustra questo esempio, vedere `CreatePolicyWithOutputProtection.java` nella directory degli strumenti della riga di comando Implementazione di riferimento [!DNL samples].

Con le API di gestione criteri DRM di Primetime potete completare le seguenti attività:

* Creare e aggiornare criteri
* Visualizza dettagli criteri DRM
* Gestisci elenchi di aggiornamento criteri DRM

Per informazioni dettagliate sull&#39;API Java, consultate *Guida di riferimento API DRM di Primetime*.

Per informazioni su Gestione criteri DRM di Primetime, vedere la guida *Utilizzo di Primetime DRM Reference Implementation*.
