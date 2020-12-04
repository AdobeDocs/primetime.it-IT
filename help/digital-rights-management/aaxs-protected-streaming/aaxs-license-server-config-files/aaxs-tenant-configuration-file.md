---
seo-title: File di configurazione tenant
title: File di configurazione tenant
uuid: 6e5c82c9-b8f5-4fca-8325-a884b2c779f7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# File di configurazione tenant {#tenant-configuration-file}

Il file di configurazione flashaccess-tenant.xml contiene impostazioni valide per un tenant specifico del server licenze. Ogni tenant ha una propria istanza di questo file di configurazione che si trova in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. Vedere la directory [!DNL configs/flashaccessserver/tenants/sampletenant] per un file di configurazione tenant di esempio.

È possibile specificare tutti i percorsi di file nel file di configurazione del tenant come percorsi assoluti o percorsi relativi alla directory di configurazione del tenant (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*).

Il file di configurazione del tenant include:

* **Credenziali**  di trasporto Specifica una o più credenziali di trasporto (certificato e chiave privata) emesse dal Adobe . Può essere specificato come percorso di un file .pfx e di una password, o come alias per una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias chiave, o entrambi. Per ulteriori informazioni sui casi in cui sono necessarie credenziali aggiuntive, vedere &quot;[Gestione degli aggiornamenti dei certificati](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; in *Utilizzo dell&#39;SDK di accesso  Adobe per la protezione dei contenuti*.
* **Credenziali**  server licenze Specifica una o più credenziali del server licenze (certificato e chiave privata) emesse dal Adobe . Può essere specificato come percorso di un file .pfx e di una password, o come alias per una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias chiave, o entrambi. Consultate Gestione degli aggiornamenti dei certificati in *Utilizzo dell&#39;SDK per l&#39;accesso ai Adobi  per la protezione dei contenuti *per ulteriori informazioni sui casi in cui sono necessarie credenziali aggiuntive.
* **Certificati**  server chiave Facoltativo. Specifica il certificato del server licenze del server chiavi emesso dal Adobe . Può essere specificato come percorso di un file .cer o come alias di un certificato memorizzato in un HSM. Questa opzione deve essere specificata per rilasciare licenze per il contenuto incluso in un pacchetto con un criterio che richiede la consegna di chiavi remote per i dispositivi iOS.
* **Autori**  personalizzati Facoltativo. Specifica le classi di authorizer personalizzate da richiamare per ogni richiesta di licenza. Se vengono specificati più autori, questi vengono richiamati nell’ordine elencato. Per ulteriori informazioni, vedere &quot;[Estensioni di autorizzazione personalizzate](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Elenco di pacchetti**  autorizzati— Facoltativo. Specifica i certificati che identificano le entità autorizzate a creare pacchetti di contenuto per questo server licenze. Se non vengono specificati certificati packager, il server rilascia licenze per il contenuto incluso in un pacchetto di qualsiasi packager.
* **Versione**  client minima supportata (consultate  *Utilizzo dell’SDK di accesso al Adobe  per la protezione del contenuto*).
* **Regole di utilizzo**

   * **Cache**  licenza Facoltativo. Specifica per quanto tempo la licenza può essere memorizzata sul client. Per impostazione predefinita, il caching delle licenze è disattivato. Per abilitare il caching delle licenze per un periodo di tempo limitato, impostare la data di fine o il numero di secondi per cui memorizzare la licenza (a partire dal momento del rilascio). Impostando il numero di secondi su 0, il caching delle licenze viene disattivato.

      Tutte le licenze rilasciate dal server per lo streaming protetto hanno un periodo di scadenza di 24 ore (86400 secondi). Questo valore si applica quindi implicitamente come limite superiore a qualsiasi data di fine o durata sia impostata anche per il caching delle licenze, con un valore massimo di 86400 secondi, anche se lo schema applica limiti superiori.

   * **Gioca a destra** — È necessario specificare almeno un diritto. Se vengono specificati più diritti, il client utilizzerà il primo diritto per il quale soddisfa tutti i requisiti.

      * **Protezione**  dell&#39;uscita Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto.
      * **Restrizioni**  per applicazioni AIR e SWF Elenco consentiti  facoltativo di applicazioni SWF e AIR che possono riprodurre il contenuto (ad es., sono consentite solo le applicazioni specificate). Le applicazioni SWF sono identificate da un URL o dal riassunto del file SWF e dal tempo massimo per consentire il download e la verifica del riassunto. Per informazioni sul calcolo del riassunto SWF, consultate la sezione &quot;SWF Hash Calculator&quot;. Le applicazioni AIR e iOS sono identificate dall&#39;ID editore e dall&#39;ID applicazione opzionale, dalla versione minima e dalla versione massima. Se non vengono specificate restrizioni per l&#39;applicazione, è possibile che il contenuto venga riprodotto da qualsiasi applicazione SWF o AIR.
      * **Limitazioni**  per i moduli DRM e Runtime Specifica il livello di protezione minimo richiesto per il modulo DRM/Runtime. Facoltativamente, include un  elenco Bloccati di versioni non consentite per riprodurre il contenuto. Le versioni dei moduli sono identificate da attributi quali il sistema operativo e/o un numero di versione. Limitazioni del modulo DRM e limitazioni del modulo runtime ora supportano i seguenti attributi aggiuntivi:

         * `oemVendor`
         * `model`
         * `screenType`

         I seguenti attributi sono ora facoltativi:

         * `osVersion`
         * `version`
      * **Requisiti**  di funzionalità del dispositivo Facoltativamente, specifica le funzionalità hardware necessarie per accedere al contenuto.
      * **Requisiti**  per il rilevamento di eventuali rotture Facoltativamente, specifica che la riproduzione non è consentita per i dispositivi sui quali viene rilevata un&#39;interruzione di connessione.



Per ulteriori dettagli, vedere i commenti nel file di configurazione del tenant di esempio.
