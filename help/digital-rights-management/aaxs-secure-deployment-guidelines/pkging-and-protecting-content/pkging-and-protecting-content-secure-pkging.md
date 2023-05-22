---
title: Imballaggio sicuro del contenuto
description: Imballaggio sicuro del contenuto
copied-description: true
exl-id: f554852c-83d9-4b31-8dde-2af577c70989
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Imballaggio sicuro del contenuto {#securely-packaging-content}

Il file di configurazione per lo strumento della riga di comando Adobe Access Media Packager richiede una credenziale PKCS12 utilizzata durante la creazione del pacchetto.

Negli strumenti della riga di comando per l&#39;implementazione di riferimento, la password per il file di credenziali PKCS12 viene memorizzata nel file flashaccess.properties in testo non crittografato. Per questo motivo, prestare particolare attenzione quando si protegge il computer che ospita il file e assicurarsi che si trovi in un ambiente sicuro. (vedere [Sicurezza fisica e accesso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

Il packager utilizza anche i certificati di trasporto del server licenze e del server licenze. L&#39;integrità e la riservatezza di tali informazioni devono essere tutelate. Solo gli enti autorizzati devono essere autorizzati ad utilizzare il confezionatore. Se una delle tue chiavi private risulta compromessa, informa immediatamente Adobe Systems Incorporated in modo che il certificato possa essere revocato.

>[!NOTE]
>
>L’API ti consente di utilizzare la stessa chiave per più parti di contenuto. Per garantire il massimo livello di sicurezza, si consiglia di utilizzare questa funzione solo per contenuti FMS a velocità multi-bit. Si sconsiglia di utilizzare la stessa chiave per più file che rappresentano contenuti diversi.

L’API per la creazione di pacchetti di accesso Adobe genera avvisi in determinate condizioni. È necessario esaminare questi avvisi per determinare se i file sono stati crittografati correttamente. I messaggi di avviso possono indicare che il criterio è scaduto, che un tag o un brano non riconosciuto non verrà crittografato, che i frammenti di filmato non verranno crittografati e che i riferimenti all&#39;interno di tali frammenti potrebbero diventare non validi e che i metadati non verranno crittografati.

Se il contenuto viene compilato utilizzando un criterio con attributi non corretti, il criterio deve essere aggiornato e reso disponibile al server licenze tramite un elenco di aggiornamento del criterio o un altro meccanismo per la distribuzione del criterio aggiornato al server. Alcuni attributi dei criteri non possono essere modificati dopo la creazione del criterio. Se questi attributi non sono corretti, richiama il contenuto dai siti di distribuzione, revoca la policy in modo che non possano essere concesse licenze future e crittografa nuovamente il contenuto.

Quando la confezione è completa, la chiave della confezione non viene esplicitamente distrutta; tuttavia, viene raccolta dai rifiuti. Pertanto, la chiave della confezione rimane presente in memoria per un periodo di tempo; è necessario proteggersi da accessi non autorizzati alla macchina e adottare misure per garantire di non esporre alcun file, come core dump, che possa rivelare queste informazioni.
