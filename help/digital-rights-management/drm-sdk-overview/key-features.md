---
title: Funzioni principali
description: Funzioni principali
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Funzioni principali{#key-features}

Adobe Primetime DRM offre le seguenti funzioni chiave:

* **Supporto streaming HLS (richiede Adobe Primetime):** Utilizza Primetime DRM con contenuti HLS che possono essere inviati in streaming a qualsiasi piattaforma supportata dal Flash o da Adobe Primetime (ad esempio desktop, iOS e Android).
* **Supporto per applicazioni iOS native (richiede Adobe Primetime):** Utilizza Primetime DRM per proteggere i video nelle applicazioni iOS.
* **Supporto per applicazioni Android native (richiede Adobe Primetime):** Utilizza Primetime DRM per proteggere i video nelle applicazioni Android.
* **Streaming protetto su Xbox (richiede Adobe Primetime)**.
* **Chiave di consegna remota di iOS (richiede Adobe Primetime):** Supporto per la distribuzione di chiavi iOS remote tramite un server chiavi multi-tenant, denominato server chiavi DRM Primetime.
* **Protezione persistente dei contenuti:** Il contenuto rimane protetto lungo tutta la catena di distribuzione. Una volta inserito nel pacchetto, il contenuto rimane protetto in qualsiasi momento e parti di esso vengono decrittografate solo al momento della riproduzione e in conformità con le regole di utilizzo.
* Poiché il contenuto è confezionato con le regole di utilizzo e le informazioni sulle licenze, la protezione si sposta sempre con il contenuto. Se i consumatori senza licenza tentano di riprodurre il contenuto, il criterio incorporato nel contenuto lo reindirizza in modo da poter acquisire una licenza valida per il contenuto.
* **Riproduzione sicura di contenuti protetti:** Gli schemi di crittografia collaudati vengono utilizzati per proteggere i contenuti da riproduzioni non autorizzate.
* **Regole di utilizzo flessibili:** Le regole di utilizzo determinano il modo in cui i consumatori possono utilizzare i contenuti protetti. Le regole di utilizzo supportate da Primetime DRM consentono diversi modelli di business, tra cui pay-per-view, noleggio di film, abbonamenti o servizi finanziati da annunci. Le regole di utilizzo sono specificate dai criteri incorporati nel contenuto durante la creazione del pacchetto o possono essere specificate dal server licenze durante l&#39;acquisizione della licenza.
* **Protezione dell&#39;output:** I controlli di protezione dell&#39;uscita possono essere utilizzati per attivare schemi di protezione come HDCP, CGMS-A o Rovi (precedentemente Macrovision) ACP. In questo modo è possibile proteggere l&#39;output dei contenuti sulle uscite digitali (ad esempio, HDMI, DVI e UDI) e analogiche (ad esempio, S-Video e Component Video).

  È possibile specificare le opzioni di protezione dell&#39;output nel criterio creato per il contenuto, consentendo o negando l&#39;accesso al contenuto in base alle funzionalità di protezione dell&#39;output di un dispositivo. Ad esempio, è possibile specificare che la protezione dell&#39;output non è richiesta per determinati contenuti, ma per contenuti video di alta qualità, impedendo l&#39;output di contenuti su sistemi operativi che non dispongono di questa funzionalità.

  Anche se queste regole vengono applicate in modo coerente su tutte le piattaforme, attualmente è possibile attivare in modo sicuro la protezione dell’output solo sulle piattaforme Windows.

* **Supporto per lo streaming dinamico:** Utilizza la funzione di streaming dinamico di Flash Media Server o Adobe HTTP Dynamic Streaming per proteggere il contenuto codificato a velocità bit multiple. Lo streaming dinamico utilizza uno streaming video che regola dinamicamente il bit rate e la qualità di riproduzione in base alla larghezza di banda disponibile, offrendo un’esperienza di utilizzo migliore. Primetime DRM consente di utilizzare la stessa chiave di crittografia dei contenuti e la stessa licenza nelle diverse codifiche della stessa risorsa.
* **Visualizzazione offline:** Il client runtime di Adobe AIR consente ai consumatori di scaricare e archiviare il contenuto per la visualizzazione successiva, indipendentemente dal fatto che il computer rimanga connesso a Internet.
* **Licenze basate su identità:** Collega le autorizzazioni alle identità utente, richiedendo ai consumatori di autenticarsi (fornendo un ID utente e una password) per poter accedere al contenuto. Le licenze basate su identità richiedono che la parte che sviluppa l&#39;applicazione client implementi l&#39;autenticazione utente come parte del flusso di lavoro di acquisizione delle licenze.
* **Concatenamento licenze:** Consente ai consumatori di estendere la durata di tutti i loro contenuti rinnovando una singola licenza root. Uno degli usi principali del concatenamento delle licenze è per i modelli di business basati su abbonamento, in cui, al termine di un periodo di abbonamento, le licenze per un numero elevato di file di contenuto possono essere rinnovate semplicemente rinnovando la licenza root.

  Le licenze radice e foglia sono associate al computer del consumatore. La licenza foglia contiene il CEK e un riferimento alla licenza radice. La licenza root può estendere i diritti concessi nella licenza foglia. Ad esempio, un consumatore può disporre di licenze foglia per 50 contenuti che scadranno alla fine di un determinato periodo di abbonamento. Se il consumatore scarica una nuova licenza root con una nuova data di scadenza, tutti i 50 contenuti possono essere riprodotti fino alla scadenza della licenza aggiornata.

  Primetime DRM 2.0 introdusse il concatenamento delle licenze in cui le licenze foglia e radice sono associate a un computer specifico. Primetime DRM 3.0 introduce una forma avanzata di concatenamento delle licenze, in cui una foglia è associata a una licenza radice e solo la licenza radice è associata a un computer o dominio specifico. Letto *Concatenamento licenze migliorato* in *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti*.

* **Rotazione chiave:** Durante la tipica creazione di pacchetti, il contenuto viene crittografato utilizzando la chiave di crittografia del contenuto (CEK) e il client ottiene una licenza contenente il CEK per utilizzare il contenuto. Quando è abilitata la rotazione delle chiavi, la chiave utilizzata per crittografare il contenuto può essere modificata in modo che venga utilizzata solo per crittografare una parte del contenuto. Letto *Rotazione tasti* in *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti*.

* **Licenze fuori banda:** Con Primetime DRM, è possibile implementare un flusso di lavoro in cui i client ottengono licenze pregenerate fuori banda, eliminando la necessità di distribuire un server licenze.
* **Supporto dominio:** In alternativa all&#39;associazione di una licenza a un dispositivo specifico, DRM di Primetime supporta l&#39;associazione di licenze a un dominio. Più dispositivi possono essere aggiunti a un dominio e ricevere un token di dominio che consente lo spostamento delle licenze tra i dispositivi del dominio. Letto *Registrazione dominio* in *Utilizzo dell’SDK Adobe Primetime DRM per la protezione dei contenuti*.

* **Crittografia parziale:** Specifica se tutti i fotogrammi o solo un sottoinsieme di fotogrammi devono essere crittografati. Sono disponibili tre livelli di crittografia: basso, medio e alto. La riduzione del livello di crittografia può ridurre il sovraccarico della CPU sui computer di fascia bassa.
* **Package di contenuto disconnesso:** La creazione di pacchetti di contenuti non richiede una connessione di rete al server licenze. Ciò garantisce la sicurezza delle operazioni back-end limitando l&#39;esposizione dei contenuti compressi che non sono ancora stati protetti.
* **Controllo del rollback dell&#39;orologio: **Primetime DRM fornisce il calcolo sicuro e preciso dell&#39;ora per rilevare il rollback dell&#39;orologio sul computer client. In questo modo vengono applicati i diritti relativi all&#39;accesso ai contenuti per un periodo di tempo specifico e viene impedito ai consumatori di sovvertire i diritti di accesso modificando l&#39;ora sul computer.
* **Individualizzazione**: consente di associare il contenuto a un computer specifico.
* **Elenco consentiti applicazione:** Consente al runtime client di garantire che il contenuto protetto venga riprodotto solo all’interno di un’applicazione SWF o AIR autorizzata.
* **Revoca dei clienti compromessi:** Il software client compromesso può essere revocato. Se il Flash Player o il runtime di Adobe AIR risultano compromessi, il servizio può essere rifiutato a tali client fino a quando non eseguono l&#39;aggiornamento a una versione più recente e più sicura del software client.
* **Più criteri per lo stesso file video:** Un singolo contenuto video può avere più criteri incorporati durante la creazione del pacchetto. Al momento del rilascio di una licenza, il server licenze può decidere quali policy utilizzare, consentendo a un distributore di contenuti di utilizzare lo stesso file protetto per diversi modelli aziendali (ad esempio noleggio e vendita elettronica).
