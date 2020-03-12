---
seo-title: Panoramica sull'utilizzo dei criteri DRM
title: Panoramica sull'utilizzo dei criteri DRM
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Panoramica {#working-with-drm-policies-overview}

I fornitori di contenuti possono applicare criteri DRM ai file multimediali utilizzando l&#39;SDK DRM di Primetime. Gli amministratori possono quindi creare, visualizzare i dettagli e aggiornare i criteri DRM utilizzando le API di gestione dei criteri.

Una raccolta di informazioni *`DRM policy`* include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Il criterio definisce il modo in cui gli utenti possono visualizzare il contenuto. Criteri DRM, cifratura e firma consentono ai fornitori di contenuti di mantenere il controllo dei contenuti indipendentemente dalla loro ampiezza di distribuzione.

Un criterio DRM funge da modello utilizzato dal server licenze per generare una licenza. Un client può anche fare riferimento al criterio DRM prima di richiedere una licenza, per determinare se il client deve richiedere all&#39;utente l&#39;autenticazione prima di inviare una richiesta di licenza al server.

Potete fornire contenuto protetto tramite Adobe Flash Media Server o un server HTTP. Gli utenti possono scaricare e riprodurre contenuto protetto in lettori personalizzati creati con l&#39;SDK DRM di Primetime.

Un criterio DRM specifica uno o più diritti concessi al client. In genere, un criterio DRM include, come minimo, *`Play Right`*. Potete anche specificare più diritti di riproduzione, ciascuno con diverse limitazioni. Quando il cliente riceve una licenza con più diritti di riproduzione, utilizza la prima licenza che soddisfa tutte le restrizioni. Ad esempio, è possibile applicare diverse impostazioni di protezione dell&#39;output su piattaforme diverse.

Per un esempio di codice che illustra questo esempio, vedete `CreatePolicyWithOutputProtection.java` nella directory Strumenti della riga di comando Implementazione di riferimento [!DNL samples] .

Con le API di gestione criteri DRM di Primetime potete completare le seguenti attività:

* Creare e aggiornare criteri
* Visualizza dettagli criteri DRM
* Gestisci elenchi di aggiornamento criteri DRM

Per informazioni dettagliate sull&#39;API Java, consultate *Primetime DRM API Reference* (Riferimento API DRM di Primetime).

Per informazioni su Gestione criteri DRM di Primetime, consulta la guida *Utilizzo delle implementazioni* di riferimento DRM di Primetime.
