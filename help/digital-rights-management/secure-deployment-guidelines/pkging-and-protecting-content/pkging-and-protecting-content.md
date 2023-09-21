---
description: Le informazioni sulla creazione di pacchetti e sulla protezione dei contenuti consentono di proteggere i contenuti.
title: Imballaggio e protezione del contenuto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Creazione di pacchetti e protezione dei contenuti {#packaging-protecting-content}

Le informazioni sulla creazione di pacchetti e sulla protezione dei contenuti consentono di proteggere i contenuti.

## Protezione del server {#securing-the-server}

È necessario proteggere fisicamente il computer in cui si verificano la gestione delle policy e la creazione di pacchetti di contenuti.

Per ulteriori informazioni, consulta [Sicurezza fisica e accesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Se l&#39;implementazione del pacchetto di contenuti richiede la connettività di rete, è necessario rafforzare il sistema operativo e implementare una soluzione firewall appropriata. Per ulteriori informazioni, consulta [Topologia di rete](../../secure-deployment-guidelines/overview/network-topology.md).

## Imballaggio sicuro del contenuto {#securely-packaging-content}

Il file di configurazione per lo strumento da riga di comando Adobe Primetime DRM Media Packager richiede una credenziale PKCS12 utilizzata durante la creazione del pacchetto.

Negli strumenti della riga di comando per l&#39;implementazione di riferimento, la password per il file di credenziali PKCS12 viene memorizzata in `flashaccess.properties` file in testo non crittografato. Per questo motivo, prestare particolare attenzione quando si protegge il computer che ospita il file e assicurarsi che si trovi in un ambiente sicuro. Per ulteriori informazioni, consulta [Sicurezza fisica e accesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Il Packager utilizza anche i certificati License Server e License Server Transport, e l&#39;integrità e la riservatezza di queste informazioni devono essere protette. Solo gli enti autorizzati devono essere autorizzati ad utilizzare il confezionatore. Se le tue chiavi private sono compromesse, informa immediatamente Adobe Systems Incorporated in modo che il certificato possa essere revocato.

>[!NOTE]
>
>L’API ti consente di utilizzare la stessa chiave per più parti di contenuto. Per garantire il massimo livello di sicurezza, è consigliabile utilizzare questa funzione solo per contenuti FMS a velocità multi-bit. Non utilizzare la stessa chiave per più file che rappresentano contenuti diversi.

L’API di packaging DRM di Primetime genera avvisi in determinate condizioni. Esaminare questi avvisi per determinare se i file sono stati crittografati correttamente. I messaggi di avviso possono essere uno dei seguenti:

* Il criterio è scaduto e non è possibile crittografare un tag o un brano non riconosciuto.
* I frammenti di filmato non possono essere crittografati e i riferimenti all’interno di tali frammenti potrebbero non essere validi.
* Impossibile crittografare i metadati.

Se il contenuto viene compilato utilizzando un criterio con attributi non corretti, il criterio deve essere aggiornato. Il criterio aggiornato deve essere reso disponibile al server licenze tramite un elenco di aggiornamento dei criteri o un altro meccanismo di consegna. Alcuni attributi dei criteri non possono essere modificati dopo la creazione del criterio. Se questi attributi non sono corretti, richiama il contenuto dai siti di distribuzione, revoca la policy in modo che non possano essere concesse licenze future e crittografa di nuovo il contenuto.

Una volta completata la creazione del package, la chiave di creazione del package viene raccolta in modo automatico e non viene eliminata in modo esplicito. Di conseguenza, la chiave di packaging rimane presente in memoria per un certo periodo di tempo. È necessario proteggersi da accessi non autorizzati al computer e assicurarsi di non esporre file, come le immagini di base, che potrebbero rivelare queste informazioni.

## Archiviazione sicura delle policy {#securely-storing-policies}

L’SDK Adobe Primetime DRM consente di sviluppare applicazioni da utilizzare per la creazione di pacchetti di contenuti e policy.

Quando crei queste applicazioni, puoi consentire ad alcuni utenti di creare e modificare le policy e limitare gli altri utenti all’applicazione delle sole policy esistenti al contenuto. È necessario implementare i controlli di accesso necessari e creare account utente con privilegi diversi per la creazione di criteri e l&#39;applicazione di criteri.

I criteri non vengono firmati o protetti da modifiche fino a quando non vengono utilizzati nel pacchetto. Se si teme che gli utenti dello strumento di creazione pacchetti possano modificare i criteri, firmare i criteri per assicurarsi che non possano essere modificati.

Per ulteriori informazioni sulla creazione di applicazioni con l’SDK, consulta API DRM di Primetime su [Riferimenti API di API Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Crittografia a chiave asimmetrica {#asymmetric-key-encryption}

La crittografia a chiave asimmetrica, detta anche crittografia a chiave pubblica, utilizza coppie di chiavi. Una chiave è per la crittografia, l&#39;altra per la decrittografia.

La chiave di decrittografia, o *`private key`*, è mantenuto segreto; la chiave di crittografia o *`public key`*, è reso disponibile a chiunque sia autorizzato a crittografare il contenuto. Chiunque abbia accesso alla chiave pubblica può crittografare il contenuto. Tuttavia, solo un utente con accesso alla chiave privata può decrittografare il contenuto. Impossibile ricostruire la chiave privata dalla chiave pubblica.

Quando si crea un pacchetto di contenuto, la chiave pubblica del server licenze viene utilizzata per crittografare la chiave di crittografia del contenuto (CEK) nei metadati DRM. È necessario assicurarsi che solo il server licenze abbia accesso alla chiave privata del server licenze. Se qualcun altro ha la chiave, può decrittografare e visualizzare il contenuto.

>[!CAUTION]
>
>Assicurarsi di ottenere il certificato del server licenze che include la chiave pubblica da un&#39;origine attendibile. In questo modo, è possibile assicurarsi che sia la chiave del server licenze e non una chiave pubblica non valida. Se gli aggressori sostituissero la loro chiave pubblica con quella del server licenze, potrebbero decifrare il contenuto.

Per ulteriori informazioni su come creare un pacchetto di contenuti, consulta [Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).
