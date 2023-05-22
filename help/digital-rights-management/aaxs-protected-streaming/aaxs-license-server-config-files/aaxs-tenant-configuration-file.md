---
title: File di configurazione tenant
description: File di configurazione tenant
copied-description: true
exl-id: 0f6cafbe-99d9-43bc-9a7f-d87c4da1f37f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# File di configurazione tenant {#tenant-configuration-file}

Il file di configurazione flashaccess-tenant.xml contiene le impostazioni applicabili a un tenant specifico del server licenze. Ogni tenant ha la propria istanza di questo file di configurazione che si trova in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. Consulta la [!DNL configs/flashaccessserver/tenants/sampletenant] per un esempio di file di configurazione tenant.

È possibile specificare tutti i percorsi dei file nel file di configurazione tenant come percorsi assoluti o percorsi relativi alla directory di configurazione del tenant (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*).

Il file di configurazione tenant include:

* **Credenziali di trasporto** — Specifica una o più credenziali di trasporto (certificato e chiave privata) emesse dall&#39;Adobe. Può essere specificato come percorso di un file con estensione pfx e una password o come alias per una credenziale archiviata in un HSM. Qui è possibile specificare diverse credenziali di questo tipo, come percorsi di file, alias chiave o entrambi. Consulta &quot;[Gestione degli aggiornamenti dei certificati](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; in *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti* per ulteriori informazioni su quando sono necessarie credenziali aggiuntive.
* **Credenziali server licenze** — Specifica una o più credenziali del server licenze (certificato e chiave privata) rilasciate dall&#39;Adobe. Può essere specificato come percorso di un file con estensione pfx e una password o come alias per una credenziale archiviata in un HSM. Qui è possibile specificare diverse credenziali di questo tipo, come percorsi di file, alias chiave o entrambi. Consulta Gestione degli aggiornamenti dei certificati in *Utilizzo dell’SDK di accesso di Adobe per la protezione del contenuto *per ulteriori informazioni su quando sono necessarie credenziali aggiuntive.
* **Certificati server chiave** — Facoltativo. Specifica il certificato del server licenze del server chiavi emesso da Adobe. Può essere specificato come percorso di un file con estensione cer o come alias di un certificato archiviato in un HSM. È necessario specificare questa opzione per emettere licenze per contenuti inclusi in un criterio che richiede la consegna della chiave remota per i dispositivi iOS.
* **Autorizzatori personalizzati** — Facoltativo. Specifica le classi di autorizzazione personalizzate da richiamare per ogni richiesta di licenza. Se sono specificati più autorizzatori, questi vengono richiamati nell&#39;ordine indicato. Per ulteriori informazioni, consulta la sezione &quot;[Estensioni di autorizzazione personalizzate](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Elenco dei Packagers autorizzati** — Facoltativo. Specifica i certificati che identificano le entità autorizzate a creare pacchetti di contenuto per questo server licenze. Se non viene specificato alcun certificato Packager, il server rilascia licenze per il contenuto inserito in un pacchetto da qualsiasi packager.
* **Versione minima client supportata** (vedere *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti*).
* **Regole di utilizzo**

   * **Caching delle licenze** — Facoltativo. Specifica per quanto tempo la licenza può essere archiviata sul client. Per impostazione predefinita, il caching delle licenze è disabilitato. Per abilitare il caching delle licenze per un periodo di tempo limitato, impostare la data di fine o il numero di secondi per i quali la licenza deve essere archiviata (a partire dal momento del rilascio della licenza). Se si imposta il numero di secondi su 0, il caching delle licenze viene disattivato.

      Tutte le licenze rilasciate dal server per lo streaming protetto hanno un periodo di scadenza di 24 ore (86400 secondi). Questo valore si applica quindi implicitamente come limite superiore a qualsiasi data di fine o durata impostata anche per il caching delle licenze, con un valore massimo di 86400 secondi, anche se lo schema applica limiti più elevati.

   * **Riproduci a destra** — Specificare almeno un diritto. Se vengono specificati più diritti, il client utilizzerà il primo diritto per il quale soddisfa tutti i requisiti.

      * **Protezione dell&#39;output** — Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto.
      * **Limitazioni per le applicazioni AIR e SWF** — elenco consentiti facoltativo di applicazioni SWF e AIR che possono riprodurre il contenuto (ovvero, sono consentite solo le applicazioni specificate). Le applicazioni SWF sono identificate da un URL o dal digest del SWF e dal tempo massimo per consentire il download e la verifica del digest. Per informazioni sul calcolo del digest SWF, consulta la sezione &quot;Calcolatore hash SWF&quot;. Le applicazioni AIR e iOS sono identificate da un ID editore e da un ID applicazione facoltativo, da una versione minima e da una versione massima. Se non viene specificata alcuna restrizione dell’applicazione, il contenuto può essere riprodotto da qualsiasi applicazione SWF o AIR.
      * **Restrizioni per i moduli DRM e runtime** — Specifica il livello di protezione minimo richiesto per il modulo DRM/Runtime. Facoltativamente include un elenco Bloccati di versioni a cui non è consentito riprodurre il contenuto. Le versioni del modulo sono identificate da attributi come il sistema operativo e/o un numero di versione. Le restrizioni per i moduli DRM e le restrizioni per i moduli runtime supportano ora i seguenti attributi aggiuntivi:

         * `oemVendor`
         * `model`
         * `screenType`

         I seguenti attributi sono ora facoltativi:

         * `osVersion`
         * `version`
      * **Requisiti di funzionalità del dispositivo** — specifica facoltativamente le funzionalità hardware necessarie per accedere al contenuto.
      * **Requisiti di rilevamento jailbreak** — Facoltativamente specifica che la riproduzione non è consentita per i dispositivi su cui viene rilevato jailbreak.



Per ulteriori dettagli, vedi i commenti nel file di configurazione del tenant di esempio.
