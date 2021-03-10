---
description: Le informazioni sull'imballaggio e la protezione dei contenuti consentono di proteggere i contenuti.
title: Imballaggio e protezione del contenuto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# Pacchetto e protezione dei contenuti {#packaging-protecting-content}

Le informazioni sull&#39;imballaggio e la protezione dei contenuti consentono di proteggere i contenuti.

## Protezione del server {#securing-the-server}

È necessario proteggere fisicamente il computer in cui si verifica la gestione dei criteri e la creazione di pacchetti di contenuti.

Per ulteriori informazioni, consulta [Sicurezza fisica e accesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Se l’implementazione del pacchetto di contenuti richiede una connettività di rete, è necessario rendere più rigido il sistema operativo e implementare una soluzione firewall appropriata. Per ulteriori informazioni, consulta [Topologia di rete](../../secure-deployment-guidelines/overview/network-topology.md).

## Confezione sicura del contenuto {#securely-packaging-content}

Il file di configurazione per lo strumento a riga di comando Adobe Primetime DRM Media Packager richiede una credenziale PKCS12 utilizzata durante la creazione del pacchetto.

Negli strumenti a tendina Implementazione di riferimento, la password per il file di credenziali PKCS12 viene memorizzata nel file `flashaccess.properties` in testo libero. Per questo motivo, prestare maggiore attenzione quando si protegge il computer che ospita questo file e assicurarsi che il computer si trovi in un ambiente sicuro. Per ulteriori informazioni, consulta [Sicurezza fisica e accesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Il imballatore utilizza anche i certificati di trasporto del server licenze e del server licenze e l&#39;integrità e la riservatezza di tali informazioni devono essere protette. È opportuno consentire l&#39;uso del condizionatore solo alle persone autorizzate. Se le tue chiavi private sono compromesse, informa immediatamente Adobe Systems Incorporated in modo che il certificato possa essere revocato.

>[!NOTE]
>
>L’API ti consente di utilizzare la stessa chiave per più parti di contenuto. Per garantire il massimo livello di sicurezza, è consigliabile utilizzare questa funzione solo per i contenuti FMS a più bit rate. Non utilizzare la stessa chiave per più file che rappresentano contenuti diversi.

L&#39;API di pacchetto DRM di Primetime invia degli avvisi in presenza di determinate condizioni. Controlla questi avvisi per determinare se i file sono stati crittografati correttamente. I messaggi di avviso possono essere uno dei seguenti:

* Il criterio è scaduto e non è possibile crittografare un tag o un brano non riconosciuto.
* Impossibile crittografare i frammenti filmato e i riferimenti all&#39;interno di tali frammenti potrebbero non essere validi.
* I metadati non possono essere crittografati.

Se il contenuto viene compilato utilizzando un criterio con attributi non corretti, è necessario aggiornare il criterio. Il criterio aggiornato deve essere reso disponibile al server licenze tramite un elenco di aggiornamento dei criteri o un altro meccanismo di consegna. Non è possibile modificare alcuni attributi del criterio dopo la creazione. Se questi attributi non sono corretti, recupera il contenuto dai siti di distribuzione, revoca il criterio in modo che non possano essere concesse licenze future e crittografa nuovamente il contenuto.

Quando l&#39;imballaggio è completo, il codice di imballaggio viene raccolto e non viene esplicitamente distrutto. Di conseguenza, il codice di imballaggio rimane presente in memoria per un certo periodo di tempo. È necessario evitare l&#39;accesso non autorizzato alla macchina e assicurarsi di non esporre file, come le immagini di base, che potrebbero rivelare queste informazioni.

## Memorizzazione sicura dei criteri {#securely-storing-policies}

L’SDK DRM di Adobe Primetime consente di sviluppare applicazioni che possono essere utilizzate per la creazione di pacchetti di contenuti e criteri.

Quando crei queste applicazioni, puoi consentire ad alcuni utenti di creare e modificare i criteri e limitare altri utenti ad applicare solo i criteri esistenti al contenuto. È necessario implementare i controlli di accesso necessari e creare account utente con privilegi diversi per la creazione dei criteri e l&#39;applicazione dei criteri.

I criteri non sono firmati o protetti da modifiche finché non vengono utilizzati in imballaggi. Se sei preoccupato che gli utenti di strumenti di imballaggio possano modificare i criteri, firma i criteri in modo che i criteri non possano essere modificati.

Per ulteriori informazioni sulla creazione di applicazioni con l&#39;SDK, consulta API DRM di Primetime su [Riferimenti API di Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Crittografia asimmetrica delle chiavi {#asymmetric-key-encryption}

La crittografia a chiave asimmetrica, detta anche crittografia a chiave pubblica, utilizza coppie di chiavi. Una chiave è per la crittografia, l&#39;altra è per la decrittografia.

Il tasto di decrittografia, o il *`private key`*, è tenuto segreto; la chiave di crittografia, o *`public key`*, viene resa disponibile a chiunque sia autorizzato a crittografare il contenuto. Chiunque abbia accesso alla chiave pubblica può crittografare il contenuto. Tuttavia, solo gli utenti con accesso alla chiave privata possono decrittografare il contenuto. Impossibile ricostruire la chiave privata dalla chiave pubblica.

Quando si crea un pacchetto di contenuto, la chiave pubblica del server licenze viene utilizzata per crittografare la chiave di crittografia del contenuto (CEK) nei metadati DRM. È necessario assicurarsi che solo il server licenze abbia accesso alla chiave privata del server licenze. Se qualcun altro ha la chiave, può decifrare e visualizzare il contenuto.

>[!CAUTION]
>
>Assicurati di ottenere il certificato del server licenze che include la chiave pubblica da un&#39;origine attendibile. In questo modo, puoi assicurarti che sia la chiave del server licenze e non una chiave pubblica non valida. Se gli aggressori dovessero sostituire la chiave pubblica del server licenze, potrebbero decifrare il contenuto.

Per ulteriori informazioni su come creare pacchetti di contenuti, consulta [Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).