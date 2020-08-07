---
description: Le informazioni sulla creazione di pacchetti e sulla protezione dei contenuti consentono di proteggere i contenuti.
seo-description: Le informazioni sulla creazione di pacchetti e sulla protezione dei contenuti consentono di proteggere i contenuti.
seo-title: Imballaggio e protezione del contenuto
title: Imballaggio e protezione del contenuto
uuid: 9bf89f86-082e-40f9-8deb-c9774a9d8e02
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# Creazione di pacchetti e protezione dei contenuti {#packaging-protecting-content}

Le informazioni sulla creazione di pacchetti e sulla protezione dei contenuti consentono di proteggere i contenuti.

## Protezione del server {#securing-the-server}

È necessario proteggere fisicamente il computer in cui si verifica la gestione dei criteri e la creazione di pacchetti di contenuti.

Per ulteriori informazioni, vedere Sicurezza [fisica e accesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Se l&#39;implementazione della creazione di pacchetti di contenuto richiede connettività di rete, è necessario rendere più rigido il sistema operativo e implementare una soluzione firewall appropriata. Per ulteriori informazioni, vedere Topologia [di](../../secure-deployment-guidelines/overview/network-topology.md)rete.

## Creazione sicura di contenuti {#securely-packaging-content}

Il file di configurazione per lo strumento della riga di comando  Adobe Primetime DRM Media Packager richiede una credenziale PKCS12 utilizzata durante la creazione del pacchetto.

Negli strumenti della riga di comando Implementazione di riferimento, la password per il file di credenziali PKCS12 viene memorizzata nel `flashaccess.properties` file in testo non visibile. Per questo motivo, prestare maggiore attenzione quando si protegge il computer che ospita questo file e assicurarsi che il computer si trovi in un ambiente protetto. Per ulteriori informazioni, vedere Sicurezza [fisica e accesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Il packager utilizza anche i certificati License Server e License Server Transport e l&#39;integrità e la riservatezza di tali informazioni devono essere protette. Solo le entità autorizzate devono poter utilizzare il packager. Se le chiavi private sono compromesse, informa immediatamente Adobe Systems Incorporated in modo che il certificato possa essere revocato.

>[!NOTE]
>
>L&#39;API consente di utilizzare la stessa chiave per più contenuti. Per garantire il massimo livello di protezione, utilizzate questa funzione solo per i contenuti FMS con bitrate multiplo. Non usate la stessa chiave per più file che rappresentano contenuti diversi.

L&#39;API Primetime DRM Packaging emette avvisi a determinate condizioni. Controllate questi avvisi per determinare se i file sono stati crittografati correttamente. I messaggi di avviso possono essere:

* Il criterio è scaduto e non è possibile crittografare un tag o una traccia non riconosciuti.
* I frammenti di filmato non possono essere crittografati e i riferimenti all&#39;interno di tali frammenti potrebbero non essere validi.
* I metadati non possono essere crittografati.

Se il contenuto è incluso in un pacchetto utilizzando un criterio con attributi non corretti, il criterio deve essere aggiornato. Il criterio aggiornato deve essere reso disponibile al server licenze tramite un elenco di aggiornamento criteri o un altro meccanismo di consegna. Alcuni attributi del criterio non possono essere modificati dopo la creazione del criterio. Se questi attributi non sono corretti, richiamate il contenuto dai siti di distribuzione, revocate il criterio in modo che non possano essere concesse licenze future e crittografate di nuovo il contenuto.

Quando il pacchetto è completo, il codice di imballaggio viene raccolto e non viene esplicitamente distrutto. Di conseguenza, il codice di imballaggio rimane presente in memoria per un certo periodo di tempo. È necessario evitare l&#39;accesso non autorizzato alla macchina e assicurarsi di non esporre i file, come i cassetti di base, che potrebbero rivelare queste informazioni.

## Criteri di memorizzazione sicura {#securely-storing-policies}

L’SDK  Adobe Primetime DRM consente di sviluppare applicazioni che possono essere utilizzate per la creazione di pacchetti di contenuti e la creazione di criteri.

Quando create queste applicazioni, potete consentire ad alcuni utenti di creare e modificare i criteri e limitare altri utenti ad applicare solo i criteri esistenti al contenuto. Dovete implementare i controlli di accesso necessari e creare account utente con privilegi diversi per la creazione dei criteri e l&#39;applicazione dei criteri.

I criteri non vengono firmati o protetti da modifiche finché non vengono utilizzati nella creazione dei pacchetti. Se siete preoccupati che gli utenti di strumenti di imballaggio possano modificare i criteri, firmate i criteri in modo da impedire che i criteri possano essere modificati.

Per ulteriori informazioni sulla creazione di applicazioni con l&#39;SDK, vedi API DRM di Primetime sui riferimenti [API Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)API.

## Cifratura delle chiavi asimmetriche {#asymmetric-key-encryption}

La crittografia delle chiavi asimmetriche, detta anche crittografia delle chiavi pubbliche, utilizza coppie di chiavi. Una chiave è per la crittografia, l&#39;altra è per la decrittazione.

La chiave di decrittazione, o la *`private key`*, è tenuta segreta; la chiave di crittografia, o la chiave, *`public key`* viene messa a disposizione di chiunque sia autorizzato a cifrare il contenuto. Chiunque abbia accesso alla chiave pubblica può cifrare il contenuto. Tuttavia, solo gli utenti con accesso alla chiave privata possono decrittografare il contenuto. Impossibile ricostruire la chiave privata dalla chiave pubblica.

Quando si crea un pacchetto di contenuto, la chiave pubblica del server licenze viene utilizzata per crittografare la chiave di crittografia del contenuto (CEK) nei metadati DRM. È necessario assicurarsi che solo il server licenze abbia accesso alla chiave privata del server licenze. Se qualcun altro ha la chiave, può decifrare e visualizzare il contenuto.

>[!CAUTION]
>
>Accertatevi di ottenere il certificato del server licenze che include la chiave pubblica da un&#39;origine affidabile. In questo modo, potete assicurarvi che si tratti della chiave del server licenze e non di una chiave pubblica fuorviante. Se gli aggressori sostituissero la chiave pubblica del server licenze, potrebbero decifrare il contenuto.

Per ulteriori informazioni su come creare pacchetti di contenuto, consultate [Utilizzo dell&#39;SDK DRM di Adobe Primetime  per la protezione dei contenuti](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).