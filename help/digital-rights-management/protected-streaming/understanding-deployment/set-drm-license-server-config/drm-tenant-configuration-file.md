---
description: Il file di configurazione flashaccess-tenant.xml include impostazioni applicabili a un tenant specifico del server licenze.
title: File di configurazione tenant
exl-id: 35ec521f-ba17-4a2d-8adb-82b2c6cbe33a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# File di configurazione tenant{#tenant-configuration-file}

Il file di configurazione flashaccess-tenant.xml include impostazioni applicabili a un tenant specifico del server licenze.

Ogni tenant supporta la propria istanza di questo file di configurazione che si trova in `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Consulta la `configs/flashaccessserver/tenants/sampletenant` per un esempio di file di configurazione tenant.

È possibile specificare tutti i percorsi dei file nel file di configurazione tenant come percorsi assoluti o come percorsi relativi alla directory di configurazione del tenant (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

Il file di configurazione tenant include:

* *Credenziali di trasporto* — Specifica una o più credenziali di trasporto (certificato e chiave privata) emesse dall&#39;Adobe. Può essere specificato come percorso di un [!DNL .pfx] e una password o un alias per una credenziale archiviata in un HSM. Qui è possibile specificare diverse credenziali di questo tipo, come percorsi di file, alias chiave o entrambi.

   Consulta *Gestione degli aggiornamenti dei certificati* in *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti* per ulteriori informazioni su quando sono necessarie credenziali aggiuntive.

* *Credenziali server licenze* — Specifica una o più credenziali del server licenze (certificato e chiave privata) emesse dall&#39;Adobe. È possibile specificare le credenziali del server licenze come percorso di un [!DNL .pfx] e una password o un alias per una credenziale archiviata in un HSM. Qui è possibile specificare diverse credenziali di questo tipo, come percorsi di file, alias chiave o entrambi.

   Consulta *Gestione degli aggiornamenti dei certificati* in *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti* per ulteriori informazioni su quando sono necessarie credenziali aggiuntive.

* *Certificati server chiave* — Facoltativamente specifica il certificato del server licenze del server chiavi emesso dall&#39;Adobe. È possibile specificare il certificato del server licenze del server chiavi come percorso di un [!DNL .cer] o un alias di un certificato memorizzato in un HSM. È necessario specificare questa opzione per emettere licenze per il contenuto fornito con un criterio DRM che richiede la consegna della chiave remota per i dispositivi iOS.

* *Autorizzatori personalizzati* — Facoltativamente specifica le classi di autorizzazione personalizzate da richiamare per ogni richiesta di licenza. Se sono specificati più autorizzatori, questi vengono richiamati nell&#39;ordine indicato.
* *Elenco dei Packagers autorizzati* — Facoltativamente specifica i certificati che identificano le entità autorizzate a creare pacchetti di contenuto per questo server licenze. Se non viene specificato alcun certificato Packager, il server rilascia licenze per il contenuto incluso in un package da qualsiasi packager. Se il server riceve una richiesta di licenza da un packager non autorizzato, la richiesta viene negata.
* *Versione minima client supportata* Consulta Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti.

* *Regole di utilizzo*

   * *Caching delle licenze* — Facoltativamente specifica per quanto tempo è possibile memorizzare la licenza sul client. Per impostazione predefinita, il caching delle licenze è disabilitato. Se si desidera abilitare il caching delle licenze per un periodo di tempo limitato, è necessario impostare la data di fine o il numero di secondi per i quali la licenza deve essere memorizzata (a partire dal momento del rilascio della licenza). Se si imposta il numero di secondi su 0, il caching delle licenze viene disattivato.

      >[!NOTE]
      >
      >Tutte le licenze rilasciate da Server per lo streaming protetto includono un periodo di scadenza di 24 ore (86400 secondi). Questo valore si applica implicitamente come limite superiore a qualsiasi data di fine o durata impostata anche per il caching delle licenze, con un valore massimo di 86400 secondi, anche se lo schema applica limiti più elevati.

   * *Riproduci a destra* — Specificare almeno un diritto. Se si specificano più diritti, il client utilizza il primo diritto che soddisfa tutti i requisiti.

      * *Protezione dell&#39;output* — Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto.
      * *Limitazioni per le applicazioni AIR e SWF* — elenco consentiti facoltativo di applicazioni SWF e AIR che possono riprodurre il contenuto, ad esempio solo le applicazioni specificate. Le applicazioni SWF sono identificate da un URL o dal digest del SWF e dal tempo massimo per consentire il download e la verifica del digest.

         Consulta *Calcolatore hash SWF* per informazioni su come calcolare il digest SWF.

         Un ID editore e un ID applicazione facoltativo, una versione minima e una versione massima identificano le applicazioni AIR e iOS. Se non specifichi alcuna restrizione dell’applicazione, qualsiasi applicazione SWF o AIR può riprodurre il contenuto.

      * *Restrizioni per i moduli DRM e runtime* — Specifica il livello di protezione minimo richiesto per il modulo DRM/Runtime. Facoltativamente include un elenco Bloccati di versioni a cui non è consentito riprodurre il contenuto. Le versioni del modulo sono identificate da attributi, come il sistema operativo e/o un numero di versione.

         Le restrizioni per i moduli DRM e le restrizioni per i moduli runtime supportano ora i seguenti attributi aggiuntivi:

         * `oemVendor`
         * `model`
         * `screenType`

         I seguenti attributi sono ora facoltativi:

         * `osVersion`
         * `version`
      * *Requisiti di funzionalità del dispositivo* — specifica facoltativamente le funzionalità hardware necessarie per accedere al contenuto.
      * *Requisiti di rilevamento jailbreak* — Facoltativamente specifica che la riproduzione non è consentita per i dispositivi su cui viene rilevato jailbreak.



Per ulteriori dettagli, vedi i commenti nel file di configurazione del tenant di esempio.
