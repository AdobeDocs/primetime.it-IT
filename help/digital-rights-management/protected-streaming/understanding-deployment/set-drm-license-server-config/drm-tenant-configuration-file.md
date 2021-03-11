---
description: Il file di configurazione flashaccess-tenant.xml include impostazioni che si applicano a un tenant specifico del server licenze.
title: File di configurazione tenant
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# File di configurazione tenant{#tenant-configuration-file}

Il file di configurazione flashaccess-tenant.xml include impostazioni che si applicano a un tenant specifico del server licenze.

Ogni tenant supporta la propria istanza di questo file di configurazione che si trova in `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Vedere la directory `configs/flashaccessserver/tenants/sampletenant` per un file di configurazione tenant di esempio.

È possibile specificare tutti i percorsi di file nel file di configurazione del tenant come percorsi assoluti o come percorsi relativi alla directory di configurazione del tenant (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

Il file di configurazione del tenant include:

* *Credenziale*  di trasporto: specifica una o più credenziali di trasporto (certificato e chiave privata) emesse dall&#39;Adobe. Può essere specificato come percorso di un file [!DNL .pfx] e di una password oppure come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias di chiave, o entrambi.

   Per ulteriori informazioni su quando sono necessarie credenziali aggiuntive, consulta *Gestione degli aggiornamenti dei certificati* in *Utilizzo dell’SDK DRM di Adobe Primetime per la protezione dei contenuti* .

* *Credenziale server licenze* : specifica una o più credenziali del server licenze (certificato e chiave privata) rilasciate dall&#39;Adobe. È possibile specificare le credenziali del server di licenza come percorso di un file [!DNL .pfx] e una password, oppure come alias di una credenziale memorizzata in un HSM. Diverse credenziali possono essere specificate qui, come percorsi di file, alias di chiave, o entrambi.

   Per ulteriori informazioni su quando sono necessarie credenziali aggiuntive, consulta *Gestione degli aggiornamenti dei certificati* in *Utilizzo dell’SDK DRM di Adobe Primetime per la protezione dei contenuti* .

* *Certificati server chiavi* : specifica facoltativamente il certificato server licenze del server chiavi rilasciato da Adobe. È possibile specificare il certificato del server licenze del server chiavi come percorso di un file [!DNL .cer] o un alias di un certificato memorizzato in un HSM. Questa opzione deve essere specificata per il rilascio di licenze per contenuti che vengono assemblati con un criterio DRM che richiede la consegna di chiavi remote per i dispositivi iOS.

* *Autorizzatori personalizzati* : specifica facoltativamente le classi di authoring personalizzate da richiamare per ogni richiesta di licenza. Se sono specificati più autori, questi vengono richiamati nell’ordine elencato.
* *Elenco di pacchetti autorizzati* : specifica facoltativamente i certificati che identificano le entità autorizzate a creare pacchetti di contenuto per questo server licenze. Se non viene specificato alcun certificato di packager, il server rilascia licenze per il contenuto imballato da qualsiasi imballatore. Se il server riceve una richiesta di licenza da un imballatore non autorizzato, la richiesta viene negata.
* *Versione client minima supportata* Consulta Utilizzo dell’SDK DRM di Adobe Primetime per la protezione dei contenuti.

* *Regole di utilizzo*

   * *Memorizzazione in cache della licenza* : specifica facoltativamente per quanto tempo è possibile memorizzare la licenza sul client. Per impostazione predefinita, il caching delle licenze è disattivato. Se si desidera abilitare il caching delle licenze per un periodo di tempo limitato, è necessario impostare la data di fine o il numero di secondi per i quali memorizzare la licenza (a partire dal momento in cui viene rilasciata la licenza). Impostando il numero di secondi su 0, si disabilita il caching delle licenze.

      >[!NOTE]
      >
      >Tutte le licenze rilasciate dal Server per lo streaming protetto includono un periodo di scadenza di 24 ore (86400 secondi). Questo valore si applica implicitamente come limite superiore a qualsiasi data o durata di fine impostata anche per il caching delle licenze, con un valore massimo di 86400 secondi, anche se lo schema applica limiti più elevati.

   * *Gioca a destra* : è necessario specificare almeno un diritto. Se specifichi più diritti, il cliente utilizza il primo diritto che soddisfa tutti i requisiti.

      * *Protezione*  output: controlla se l&#39;output su dispositivi di rendering esterni deve essere protetto.
      * *Restrizioni per applicazioni AIR e SWF* : elenco consentiti facoltativo di applicazioni SWF e AIR che possono riprodurre il contenuto (ad esempio, sono consentite solo le applicazioni specificate). Le applicazioni SWF sono identificate da un URL o dal riassunto del SWF e dal tempo massimo per consentire il download e la verifica del riassunto.

         Per informazioni su come calcolare il digest SWF, vedere *Calcolatore hash SWF*.

         Un ID editore e un ID applicazione opzionale, la versione minima e la versione massima identificano le applicazioni AIR e iOS. Se non si specificano limitazioni dell’applicazione, qualsiasi applicazione SWF o AIR può riprodurre il contenuto.

      * *Restrizioni*  al modulo DRM e Runtime: specifica il livello di sicurezza minimo richiesto per il modulo DRM/Runtime. Facoltativamente include un elenco Bloccati di versioni che non sono autorizzate a riprodurre il contenuto. Le versioni del modulo sono identificate da attributi quali il sistema operativo e/o un numero di versione.

         Restrizioni al modulo DRM e restrizioni al modulo runtime ora supportano i seguenti attributi aggiuntivi:

         * `oemVendor`
         * `model`
         * `screenType`

         I seguenti attributi sono ora facoltativi:

         * `osVersion`
         * `version`
      * *Requisiti*  di funzionalità del dispositivo: specifica facoltativamente le funzionalità hardware necessarie per accedere ai contenuti.
      * *Requisiti*  di rilevamento jailbreak: indica facoltativamente che la riproduzione non è consentita per i dispositivi in cui viene rilevato jailbreak.



Per ulteriori informazioni, consulta i commenti nel file di configurazione del tenant di esempio.
