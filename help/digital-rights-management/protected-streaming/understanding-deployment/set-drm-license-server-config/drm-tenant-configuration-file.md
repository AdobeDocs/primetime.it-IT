---
description: Il file di configurazione flashaccess-tenant.xml include impostazioni valide per un tenant specifico del server licenze.
seo-description: Il file di configurazione flashaccess-tenant.xml include impostazioni valide per un tenant specifico del server licenze.
seo-title: File di configurazione tenant
title: File di configurazione tenant
uuid: bc9ee4a1-63b6-4362-9929-3e9fe8251075
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# File di configurazione tenant{#tenant-configuration-file}

Il file di configurazione flashaccess-tenant.xml include impostazioni valide per un tenant specifico del server licenze.

Ogni tenant supporta la propria istanza di questo file di configurazione che si trova in [!DNL &lt;LicenseServer.ConfigRoot>/flashaccessserver/locants/<tenantname>]. Vedere la [!DNL configs/flashaccessserver/tenants/sampletenant] directory per un file di configurazione tenant di esempio.

È possibile specificare tutti i percorsi di file nel file di configurazione del tenant come percorsi assoluti o come percorsi relativi alla directory di configurazione del tenant ( [!DNL &lt;LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>]).

Il file di configurazione del tenant include:

* *Credenziali* di trasporto — Specifica una o più credenziali di trasporto (certificato e chiave privata) emesse da Adobe. Può essere specificato come percorso di un [!DNL .pfx] file e di una password, o come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias chiave, o entrambi.

   Consultate *Gestione degli aggiornamenti* dei certificati in *Utilizzo di Adobe Primetime DRM SDK per la protezione dei contenuti* per ulteriori informazioni sui casi in cui sono necessarie credenziali aggiuntive.

* *Credenziali* server licenze — Specifica una o più credenziali server licenze (certificato e chiave privata) rilasciate da Adobe. È possibile specificare le credenziali del server di licenze come percorso di un [!DNL .pfx] file e una password, oppure un alias per una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias chiave, o entrambi.

   Consultate *Gestione degli aggiornamenti* dei certificati in *Utilizzo di Adobe Primetime DRM SDK per la protezione dei contenuti* per ulteriori informazioni sui casi in cui sono necessarie credenziali aggiuntive.

* *Certificati* server chiave — Facoltativamente, specifica il certificato Server licenze del server chiavi emesso da Adobe. È possibile specificare il certificato Server licenze del server chiavi come percorso di un [!DNL .cer] file o alias di un certificato memorizzato in un HSM. Questa opzione deve essere specificata per rilasciare licenze per il contenuto fornito con un criterio DRM che richiede la consegna di chiavi remote per i dispositivi iOS.

* *Autori* personalizzati — Facoltativamente, specifica le classi di authorizer personalizzate da richiamare per ogni richiesta di licenza. Se vengono specificati più autori, questi vengono richiamati nell’ordine elencato.
* *Elenco dei pacchetti* autorizzati — Facoltativamente, specifica i certificati che identificano le entità autorizzate a creare pacchetti di contenuto per questo server licenze. Se non vengono specificati certificati packager, il server rilascia licenze per il contenuto incluso in un pacchetto di qualsiasi packager. Se il server riceve una richiesta di licenza da un packager non autorizzato, la richiesta viene rifiutata.
* *Versione* client minima supportata Consultate Utilizzo dell’SDK DRM di Adobe Primetime per la protezione dei contenuti.

* *Regole di utilizzo*

   * *Memorizzazione delle licenze* — Facoltativamente, specifica per quanto tempo è possibile memorizzare la licenza sul client. Per impostazione predefinita, il caching delle licenze è disattivato. Se si desidera abilitare il caching delle licenze per un periodo di tempo limitato, è necessario impostare la data di fine o il numero di secondi per i quali memorizzare la licenza (a partire dal momento in cui viene rilasciata). Impostando il numero di secondi su 0, il caching delle licenze viene disattivato.

      >[!NOTE]
      >
      >Tutte le licenze rilasciate da Server for Protected Streaming includono un periodo di scadenza di 24 ore (86400 secondi). Questo valore si applica implicitamente come limite superiore a qualsiasi data o durata di fine sia impostata anche per il caching delle licenze, con un valore massimo di 86400 secondi, anche se lo schema applica limiti superiori.

   * *Gioca a destra* — È necessario specificare almeno un diritto. Se specificate più diritti, il client utilizza il primo diritto che soddisfa tutti i requisiti.

      * *Protezione* dell&#39;uscita Controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto.
      * *Restrizioni per applicazioni AIR e SWF* — L&#39;opzione consente l&#39;elenco di applicazioni SWF e AIR che possono riprodurre il contenuto (ad esempio, sono consentite solo le applicazioni specificate). Le applicazioni SWF sono identificate da un URL o dal riassunto del file SWF e dal tempo massimo per consentire il download e la verifica del riassunto.

         Per informazioni su come calcolare il riassunto SWF, consultate *SWF Hash Calculator* .

         L&#39;ID editore e l&#39;ID applicazione opzionale, la versione minima e la versione massima identificano le applicazioni AIR e iOS. Se non specificate alcuna limitazione per l’applicazione, qualsiasi applicazione SWF o AIR può riprodurre il contenuto.

      * *Limitazioni* per i moduli DRM e Runtime Specifica il livello di protezione minimo richiesto per il modulo DRM/Runtime. Facoltativamente, include un elenco di blocchi di versioni alle quali non è consentito riprodurre il contenuto. Le versioni dei moduli sono identificate da attributi, ad esempio sistema operativo e/o numero di versione.

         Limitazioni del modulo DRM e limitazioni del modulo runtime ora supportano i seguenti attributi aggiuntivi:

         * `oemVendor`
         * `model`
         * `screenType`
         I seguenti attributi sono ora facoltativi:

         * `osVersion`
         * `version`
      * *Requisiti* di funzionalità del dispositivo — Facoltativamente, specifica le funzionalità hardware necessarie per accedere al contenuto.
      * *Requisiti* per l&#39;individuazione delle rotture Facoltativamente, specifica che la riproduzione non è consentita per i dispositivi sui quali viene rilevata un&#39;interruzione di connessione.



Per ulteriori dettagli, vedere i commenti nel file di configurazione del tenant di esempio.
