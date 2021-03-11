---
title: Funzioni principali
description: Funzioni principali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---


# Funzioni principali{#key-features}

Adobe Primetime DRM offre le seguenti funzionalità principali:

* **Supporto per lo streaming HLS (richiede Adobe Primetime):** utilizza Primetime DRM con contenuti HLS che possono essere trasmessi in streaming a qualsiasi piattaforma supportata da Flash o Adobe Primetime (ad esempio Desktop, iOS e Android).
* **Supporto nativo per applicazioni iOS (richiede Adobe Primetime):** utilizza Primetime DRM per proteggere il video nelle applicazioni iOS.
* **Supporto nativo per applicazioni Android (richiede Adobe Primetime):** utilizza Primetime DRM per proteggere il video nelle applicazioni Android.
* **Streaming protetto su Xbox (richiede Adobe Primetime)**.
* **Distribuzione remota di chiavi iOS (richiede Adobe Primetime):**  supporto per la distribuzione di chiavi iOS remote tramite un server di chiavi multi-tenant, denominato server di chiavi DRM di Primetime.
* **Protezione persistente dei contenuti:** il contenuto rimane protetto lungo tutta la catena di distribuzione. Una volta che il contenuto viene assemblato, rimane sempre protetto e parti di esso vengono decrittografate solo al momento della riproduzione e in conformità con le regole di utilizzo.
* Poiché il contenuto è compilato con regole di utilizzo e informazioni sulla licenza, la protezione viaggia sempre con il contenuto. Se i consumatori senza licenza tentano di riprodurre il contenuto, i criteri incorporati nel contenuto li reindirizzano in modo da poter acquisire una licenza valida per il contenuto.
* **Riproduzione sicura di contenuti protetti:** gli schemi di crittografia collaudati vengono utilizzati per proteggere i contenuti dalla riproduzione non autorizzata.
* **Regole di utilizzo flessibili:** le regole di utilizzo determinano come i consumatori possono utilizzare i contenuti protetti. Le regole di utilizzo supportate da Primetime DRM consentono diversi modelli di business, tra cui pay-per-view, noleggio film, abbonamenti o servizi finanziati da annunci. Le regole di utilizzo sono specificate dal criterio incorporato nel contenuto durante la creazione del pacchetto oppure possono essere specificate dal server licenze durante l&#39;acquisizione della licenza.
* **Protezione dell&#39;uscita:** i controlli di protezione dell&#39;uscita possono essere utilizzati per attivare sistemi di protezione come HDCP, CGMS-A o Rovi (precedentemente Macrovision) ACP. Questo consente di proteggere l&#39;uscita dei contenuti dalle uscite digitali (ad esempio, HDMI, DVI e UDI) e analogiche (ad esempio, S-Video e Component Video).

   È possibile specificare le opzioni di protezione dell’output nel criterio creato per il contenuto, consentendo o negando l’accesso al contenuto in base alle funzionalità di protezione dell’output del dispositivo. Ad esempio, è possibile specificare che la protezione dell&#39;output non è necessaria per determinati contenuti, ma richiede la protezione dell&#39;output per contenuti video premium, impedendo l&#39;output di contenuti su sistemi operativi privi di questa funzionalità.

   Sebbene queste regole siano applicate in modo coerente in tutte le piattaforme, al momento è solo possibile attivare in modo sicuro la protezione dell&#39;output sulle piattaforme Windows.

* **Supporto per lo streaming dinamico:** utilizza la funzione di streaming dinamico di Flash Media Server o Adobe HTTP Dynamic Streaming per proteggere i contenuti codificati a più bit rate. Lo streaming dinamico utilizza un flusso video che regola dinamicamente il bit rate e la qualità di riproduzione in base alla larghezza di banda disponibile, offrendo un&#39;esperienza utente migliore. DRM di Primetime consente l’utilizzo della stessa chiave di crittografia dei contenuti e della stessa licenza nelle diverse codifiche della stessa risorsa.
* **Visualizzazione offline:** il client runtime Adobe AIR consente ai consumatori di scaricare e archiviare i contenuti per una visualizzazione successiva, indipendentemente dal fatto che il computer rimanga connesso o meno a Internet.
* **Licenza basata su identità:** collega le autorizzazioni alle identità degli utenti, richiedendo ai consumatori di effettuare l’autenticazione (fornendo un ID utente e una password) per accedere ai contenuti. La licenza basata su identità richiede che la parte che sviluppa l’applicazione client implementi l’autenticazione utente come parte del flusso di lavoro di acquisizione della licenza.
* **Concatena delle licenze:** consente ai consumatori di prolungare la vita di tutti i loro contenuti rinnovando una singola licenza root. Uno degli usi principali della concatenazione delle licenze è per i modelli di business basati su abbonamento, dove, al termine di un periodo di abbonamento, le licenze a un gran numero di file di contenuto possono essere rinnovate semplicemente rinnovando la licenza radice.

   Le licenze radice e foglia sono legate al computer del consumatore. La licenza foglia contiene il CEK e un riferimento alla licenza radice. La licenza radice può estendere i diritti concessi nella licenza foglia. Ad esempio, un consumatore può avere licenze per 50 contenuti che scadranno al termine di un determinato periodo di abbonamento. Se il consumatore scarica una nuova licenza principale con una nuova data di scadenza, è possibile riprodurre tutti e 50 i contenuti fino alla scadenza della licenza aggiornata.

   Primetime DRM 2.0 ha introdotto la concatenazione di licenze in cui sia le licenze foglia che radice sono legate a una macchina specifica. Primetime DRM 3.0 introduce una forma avanzata di concatenamento delle licenze, in cui una foglia è associata a una licenza root e solo la licenza root è associata a una macchina o a un dominio specifici. Leggi *Concatenamento licenze avanzato* in *Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti*.

* **Rotazione delle chiavi:** durante la tipica creazione di pacchetti, il contenuto viene crittografato utilizzando la chiave di crittografia dei contenuti (CEK) e il client ottiene una licenza contenente la CEK per utilizzare il contenuto. Quando la rotazione delle chiavi è abilitata, la chiave utilizzata per crittografare il contenuto può essere modificata in modo che la chiave venga utilizzata solo per crittografare una parte del contenuto. Leggi *Rotazione chiave* in *Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti*.

* **Licenze fuori banda:** con Primetime DRM, è possibile implementare un flusso di lavoro in cui i clienti ottengono licenze pre-generate fuori banda, eliminando la necessità di distribuire un server licenze.
* **Supporto del dominio:** in alternativa al binding di una licenza a un dispositivo specifico, Primetime DRM supporta il binding delle licenze a un dominio. Più dispositivi possono unire un dominio e ricevere un token di dominio che consente lo spostamento delle licenze tra i dispositivi del dominio. Leggi *Registrazione dominio* in *Utilizzo dell&#39;SDK DRM di Adobe Primetime per la protezione dei contenuti*.

* **Crittografia parziale:** specifica se tutti i frame, o solo un sottoinsieme di frame, devono essere crittografati. Sono disponibili tre livelli di crittografia: bassa, media e alta. La riduzione del livello di crittografia può ridurre il sovraccarico della CPU sui computer di fascia inferiore.
* **Pacchetto di contenuto disconnesso:** la creazione di pacchetti di contenuto non richiede una connessione di rete al server licenze. Questo consente operazioni back-end sicure limitando l&#39;esposizione di contenuti compressi non ancora protetti.
* **Controllo del rollback dell&#39;orologio: **Primetime DRM fornisce un calcolo sicuro e accurato del tempo necessario per rilevare il rollback dell&#39;orologio sul computer client. In questo modo vengono applicati i diritti relativi all’accesso ai contenuti per un periodo di tempo specifico e i consumatori non possono sovvertire i diritti di accesso modificando il tempo sul computer.
* **Individualizzazione**: Consente il binding del contenuto a un computer specifico.
* **Elenco consentiti di applicazione:** consente al runtime client di garantire che il contenuto protetto venga riprodotto solo all’interno di un’applicazione SWF o AIR autorizzata.
* **Revoca dei client compromessi:** il software client compromesso può essere revocato. Se il runtime di Flash Player o Adobe AIR è stato determinato come compromesso, il servizio può essere rifiutato a tali client fino a quando non effettuano l’aggiornamento a una versione più recente e più sicura del software client.
* **Criteri multipli per lo stesso file video:** un singolo contenuto video può avere più criteri incorporati durante la creazione del pacchetto. Quando si rilascia una licenza, il server licenze può decidere quale delle politiche utilizzare, consentendo a un distributore di contenuti di utilizzare lo stesso file protetto per diversi modelli di business (ad esempio noleggio e vendita elettronica).