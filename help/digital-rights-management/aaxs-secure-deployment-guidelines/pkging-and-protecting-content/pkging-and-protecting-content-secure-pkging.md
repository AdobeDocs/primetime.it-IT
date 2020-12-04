---
seo-title: Creazione sicura di contenuti
title: Creazione sicura di contenuti
uuid: a5e7cc17-353b-47d1-b89c-a2ba3c9faca1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Creazione sicura di pacchetti di contenuto {#securely-packaging-content}

Il file di configurazione per lo strumento della riga di comando  Access Media Packager richiede una credenziale PKCS12 utilizzata durante la creazione del pacchetto.

Negli strumenti della riga di comando Implementazione di riferimento, la password per il file di credenziali PKCS12 viene memorizzata nel file flashaccess.properties in un testo libero. Per questo motivo, prestare maggiore attenzione quando si protegge il computer che ospita questo file, e assicurarsi che si trovi in un ambiente sicuro. (Vedere [Sicurezza fisica e accesso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

Il packager utilizza anche i certificati License Server e License Server Transport. L&#39;integrità e la riservatezza di tali informazioni devono essere protette. Solo le entità autorizzate devono poter utilizzare il packager. Se una delle chiavi private è compromessa, informa immediatamente Adobe Systems Incorporated in modo che il certificato possa essere revocato.

>[!NOTE]
>
>L&#39;API consente di utilizzare la stessa chiave per più contenuti. Per garantire il massimo livello di sicurezza, si consiglia di utilizzare questa funzione solo per i contenuti FMS con bitrate multiplo. Non è consigliabile utilizzare la stessa chiave per più file che rappresentano un contenuto diverso.

L&#39;API  Adobe Access Packaging emette avvisi a determinate condizioni. È necessario esaminare questi avvisi per determinare se i file sono stati crittografati correttamente. I messaggi di avviso potrebbero indicare che il criterio è scaduto, che un tag o una traccia non riconosciuti non saranno crittografati, che i frammenti di filmato non saranno crittografati (e che i riferimenti all&#39;interno di tali frammenti potrebbero non essere validi) e che i metadati non saranno crittografati.

Se il contenuto è incluso in un pacchetto utilizzando un criterio con attributi non corretti, il criterio deve essere aggiornato e il criterio aggiornato deve essere reso disponibile al server licenze tramite un elenco di aggiornamento criteri o un altro meccanismo per la distribuzione del criterio aggiornato al server. Alcuni attributi del criterio non possono essere modificati dopo la creazione del criterio. Se questi attributi non sono corretti, richiamate il contenuto dai siti di distribuzione, revocate il criterio in modo che non possano essere concesse licenze future e recrittografate il contenuto.

Quando l&#39;imballaggio è completo, il codice di imballaggio non è esplicitamente distrutto; tuttavia, viene raccolta i rifiuti. Pertanto, il codice di imballaggio rimane presente in memoria per un periodo di tempo; è necessario evitare l&#39;accesso non autorizzato alla macchina e fare in modo di non esporre i file, come i cassetti di base, che potrebbero rivelare tali informazioni.
