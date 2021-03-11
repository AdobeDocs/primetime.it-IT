---
title: File di configurazione tenant
description: File di configurazione tenant
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# File di configurazione tenant {#tenant-configuration-file}

Il file di configurazione flashaccess-tenant.xml contiene impostazioni che si applicano a un tenant specifico del server licenze. Ogni tenant ha la propria istanza di questo file di configurazione che si trova in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. Vedere la directory [!DNL configs/flashaccessserver/tenants/sampletenant] per un file di configurazione tenant di esempio.

È possibile specificare tutti i percorsi di file nel file di configurazione del tenant come percorsi assoluti o percorsi relativi alla directory di configurazione del tenant (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*).

Il file di configurazione del tenant include:

* **Credenziale**  di trasporto: specifica una o più credenziali di trasporto (certificato e chiave privata) emesse dall&#39;Adobe. Può essere specificato come percorso di un file .pfx e di una password oppure come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias di chiave, o entrambi. Per ulteriori informazioni su quando sono necessarie credenziali aggiuntive, consulta &quot;[Gestione degli aggiornamenti dei certificati](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; in *Utilizzo dell’SDK per l’accesso ad Adobe per la protezione dei contenuti* .
* **Credenziale server licenze** : specifica una o più credenziali del server licenze (certificato e chiave privata) emesse da Adobe. Può essere specificato come percorso di un file .pfx e di una password oppure come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias di chiave, o entrambi. Per ulteriori informazioni su quando sono necessarie credenziali aggiuntive, consulta Gestione degli aggiornamenti dei certificati in *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione del contenuto *per ulteriori informazioni.
* **Certificati server chiave**  - Facoltativo. Specifica il certificato del server licenze del server chiavi rilasciato da Adobe. Può essere specificato come percorso di un file .cer o di un alias di un certificato memorizzato in un HSM. Questa opzione deve essere specificata per rilasciare licenze per contenuti inclusi in un pacchetto con un criterio che richiede la consegna di chiavi remote per dispositivi iOS.
* **Autori personalizzati**  - Facoltativo. Specifica le classi di authoring personalizzate da richiamare per ogni richiesta di licenza. Se sono specificati più autori, questi vengono richiamati nell’ordine elencato. Per ulteriori informazioni, consulta &quot;[Estensioni di autorizzazione personalizzate](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Elenco dei pacchetti**  autorizzati— Facoltativo. Specifica i certificati che identificano le entità autorizzate a creare pacchetti di contenuto per questo server licenze. Se non viene specificato alcun certificato di packager, il server rilascia licenze per il contenuto imballato da qualsiasi imballatore.
* **Versione client minima supportata**  (consulta  *Utilizzo dell’SDK per accesso Adobe per la protezione dei contenuti*).
* **Regole di utilizzo**

   * **Memorizzazione in cache delle licenze**  - Facoltativo. Specifica per quanto tempo è possibile memorizzare la licenza sul client. Per impostazione predefinita, il caching delle licenze è disattivato. Per abilitare il caching delle licenze per un periodo di tempo limitato, impostare la data di fine o il numero di secondi per i quali memorizzare la licenza (a partire dal momento del rilascio della licenza). Impostando il numero di secondi su 0, si disabilita il caching delle licenze.

      Tutte le licenze rilasciate dal Server per lo streaming protetto hanno un periodo di scadenza di 24 ore (86400 secondi). Questo valore si applica quindi implicitamente come limite superiore a qualsiasi data o durata di fine impostata anche per il caching delle licenze, con un valore massimo di 86400 secondi, anche se lo schema applica limiti più elevati.

   * **Gioca a destra** : è necessario specificare almeno un diritto. Se vengono specificati più diritti, il client utilizzerà il primo diritto per il quale soddisfa tutti i requisiti.

      * **Protezione**  output: controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto.
      * **Restrizioni per applicazioni AIR e SWF** : elenco consentiti facoltativo di applicazioni SWF e AIR che possono riprodurre il contenuto (ad esempio, sono consentite solo le applicazioni specificate). Le applicazioni SWF sono identificate da un URL o dal riassunto del SWF e dal tempo massimo per consentire il download e la verifica del riassunto. Per informazioni sul calcolo del riassunto SWF, vedere la sezione &quot;Calcolatore hash SWF&quot;. Le applicazioni AIR e iOS sono identificate da un ID editore e dall’ID applicazione opzionale, dalla versione minima e dalla versione massima. Se non vengono specificate restrizioni per l’applicazione, è possibile che il contenuto venga riprodotto da qualsiasi applicazione SWF o AIR.
      * **Restrizioni**  al modulo DRM e Runtime: specifica il livello di sicurezza minimo richiesto per il modulo DRM/Runtime. Facoltativamente include un elenco Bloccati di versioni che non sono autorizzate a riprodurre il contenuto. Le versioni del modulo sono identificate da attributi quali il sistema operativo e/o un numero di versione. Restrizioni al modulo DRM e restrizioni al modulo runtime ora supportano i seguenti attributi aggiuntivi:

         * `oemVendor`
         * `model`
         * `screenType`

         I seguenti attributi sono ora facoltativi:

         * `osVersion`
         * `version`
      * **Requisiti**  di funzionalità del dispositivo: specifica facoltativamente le funzionalità hardware necessarie per accedere ai contenuti.
      * **Requisiti**  di rilevamento jailbreak: indica facoltativamente che la riproduzione non è consentita per i dispositivi in cui viene rilevato jailbreak.



Per ulteriori informazioni, consulta i commenti nel file di configurazione del tenant di esempio.
