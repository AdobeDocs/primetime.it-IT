---
title: Confezione sicura del contenuto
description: Confezione sicura del contenuto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Confezione sicura del contenuto {#securely-packaging-content}

Il file di configurazione per lo strumento a riga di comando Adobe Access Media Packager richiede una credenziale PKCS12 utilizzata durante la creazione del pacchetto.

Negli strumenti della riga di comando Implementazione di riferimento, la password per il file di credenziali PKCS12 viene memorizzata nel file flashaccess.properties in testo libero. Per questo motivo, prestare maggiore attenzione durante la protezione del computer che ospita questo file e assicurarsi che si trovi in un ambiente sicuro. (Vedere [Sicurezza fisica e accesso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

Il packager utilizza anche i certificati di trasporto del server licenze e del server licenze. L&#39;integrità e la riservatezza di tali informazioni devono essere protette. È opportuno consentire l&#39;uso del condizionatore solo alle persone autorizzate. Se una delle tue chiavi private è compromessa, informa immediatamente Adobe Systems Incorporated in modo che il certificato possa essere revocato.

>[!NOTE]
>
>L’API ti consente di utilizzare la stessa chiave per più parti di contenuto. Per garantire il massimo livello di sicurezza, si consiglia di utilizzare questa funzione solo per i contenuti FMS a più bit rate. Si sconsiglia di utilizzare la stessa chiave per più file che rappresentano contenuti diversi.

L&#39;API Adobe Access Packaging invia avvisi in presenza di determinate condizioni. È necessario esaminare questi avvisi per determinare se i file sono stati crittografati correttamente. I messaggi di avviso potrebbero indicare che il criterio è scaduto, che un tag o una traccia non riconosciuti non verranno crittografati, che i frammenti filmato non verranno crittografati (e che i riferimenti all’interno di tali frammenti potrebbero non essere validi) e che i metadati non verranno crittografati.

Se il contenuto viene compilato utilizzando un criterio con attributi non corretti, è necessario aggiornare il criterio e rendere disponibile il criterio aggiornato al server licenze tramite un elenco di aggiornamento dei criteri o un altro meccanismo per la distribuzione del criterio aggiornato al server. Non è possibile modificare alcuni attributi del criterio dopo la creazione. Se questi attributi non sono corretti, puoi estrarre il contenuto dai siti di distribuzione, revocare il criterio in modo che non possano essere concesse licenze future e crittografare nuovamente il contenuto.

Quando l&#39;imballaggio è completo, il codice di imballaggio non viene esplicitamente distrutto; tuttavia, viene raccolta i rifiuti. Pertanto, il codice di imballaggio rimane presente in memoria per un periodo di tempo; è necessario evitare l&#39;accesso non autorizzato alla macchina e fare in modo di non esporre alcun file, come le immagini di base, che possa rivelare queste informazioni.
