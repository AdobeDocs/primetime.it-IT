---
seo-title: Funzioni principali
title: Funzioni principali
uuid: b1bded0f-4e45-4ff8-a7ce-dac3d3ec0ab0
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# Funzioni principali {#key-features}

In Adobe Access sono disponibili le seguenti funzionalità principali:

* **Supporto per lo streaming HLS (richiede Adobe Primetime):** Utilizzate Adobe Access DRM con contenuto HLS che può essere trasmesso in streaming a qualsiasi piattaforma supportata da Flash o Adobe Primetime (ad esempio, desktop, iOS e Android).
* **Supporto delle applicazioni iOS native (richiede Adobe Primetime):** Utilizzate Adobe Access DRM per proteggere il video nelle applicazioni iOS.
* **Supporto delle applicazioni Android native (richiede Adobe Primetime):** Utilizzate Adobe Access DRM per proteggere il video nelle applicazioni Android.
* **Streaming protetto su Xbox (richiede Adobe Primetime)**.
* **Distribuzione remota delle chiavi iOS (richiede Adobe Primetime):** Supporto per la distribuzione delle chiavi iOS remote tramite un server di chiavi multi-tenant, denominato Adobe Access Key Server.
* **Protezione del contenuto persistente:** Il contenuto rimane protetto in tutta la catena di distribuzione. Una volta creato il pacchetto, il contenuto rimane sempre protetto e parti di esso vengono decrittografate solo al momento della riproduzione e in conformità alle regole di utilizzo.
* Poiché il contenuto è fornito con regole di utilizzo e informazioni sulla licenza, la protezione viaggia sempre con il contenuto. Se i consumatori senza licenza tentano di riprodurre il contenuto, il criterio incorporato nel contenuto li reindirizzerà in modo che possano acquisire una licenza valida per il contenuto.
* **Riproduzione sicura dei contenuti protetti: **Gli schemi di crittografia collaudati sono utilizzati per proteggere i contenuti dalla riproduzione non autorizzata.
* **Regole di utilizzo flessibili:** Le regole di utilizzo determinano in che modo i consumatori possono utilizzare il contenuto protetto. Le regole di utilizzo supportate da Adobe Access consentono la creazione di diversi modelli aziendali, tra cui pay-per-view, noleggio film, iscrizioni o servizi con finanziamento di annunci. Le regole di utilizzo sono specificate dal criterio incorporato nel contenuto durante la creazione del pacchetto oppure possono essere specificate dal server licenze durante l&#39;acquisizione della licenza.
* **Protezione dell&#39;uscita:** I controlli di protezione dell&#39;uscita possono essere utilizzati per attivare programmi di protezione come HDCP, CGMS-A o Rovi (ex Macrovision) ACP. In questo modo è possibile proteggere l&#39;uscita dei contenuti dalle uscite digitali (ad esempio, HDMI, DVI e UDI) e analogiche (ad esempio, S-Video e Component Video).

   Potete specificare le opzioni di protezione dell&#39;output nel criterio creato per il contenuto, consentendo o meno l&#39;accesso al contenuto in base alle funzionalità di protezione dell&#39;output del dispositivo. Ad esempio, potete specificare che la protezione dell&#39;output non è necessaria per determinati contenuti, ma che è necessaria la protezione dell&#39;output per i contenuti video premium, impedendo l&#39;output dei contenuti sui sistemi operativi che non dispongono di tale funzionalità.

   Sebbene queste regole siano applicate in modo coerente su tutte le piattaforme, al momento è possibile attivare la protezione dell&#39;output solo in modo sicuro sulle piattaforme Windows.

* **Supporto per lo streaming dinamico: **Utilizzate la funzione di streaming dinamico di Flash Media Server o Adobe HTTP Dynamic Streaming per proteggere i contenuti codificati a più bitrate. Lo streaming dinamico utilizza un flusso video che regola dinamicamente il bitrate e la qualità di riproduzione in base alla larghezza di banda disponibile, offrendo agli utenti un&#39;esperienza migliore. Adobe Access consente di utilizzare la stessa chiave di crittografia e la stessa licenza per le diverse codifiche della stessa risorsa.
* **Visualizzazione offline:** Il client runtime Adobe AIR consente ai consumatori di scaricare e archiviare il contenuto per la visualizzazione successiva, indipendentemente dal fatto che il computer resti connesso a Internet.
* **Licenze basate su identità:** Collega le autorizzazioni alle identità degli utenti, richiedendo ai consumatori di autenticarsi (fornendo un ID utente e una password) per poter accedere ai contenuti. La licenza basata sull&#39;identità richiede che la parte che sta sviluppando l&#39;applicazione client implementi l&#39;autenticazione utente come parte del flusso di lavoro di acquisizione della licenza.
* **Concatenamento licenza:** Consente ai consumatori di estendere la durata di tutti i loro contenuti rinnovando una singola licenza root. Uno degli usi principali della concatenazione delle licenze è per i modelli aziendali basati su abbonamento, dove, alla fine di un periodo di abbonamento, le licenze per un elevato numero di file di contenuto possono essere rinnovate semplicemente rinnovando la licenza principale.

   Le licenze radice e foglia sono entrambe associate al computer del consumatore. La licenza foglia contiene il CEK e un riferimento alla licenza radice. La licenza root può estendere i diritti concessi nella licenza foglia. Ad esempio, un consumatore può avere licenze per 50 contenuti che scadranno alla fine di un determinato periodo di iscrizione. Se il consumatore scarica una nuova licenza principale con una nuova data di scadenza, tutti i 50 contenuti possono essere riprodotti fino alla scadenza della licenza aggiornata.

   Adobe Access 2.0 ha introdotto la concatenazione delle licenze in cui le licenze foglia e radice sono associate a un computer specifico. Adobe Access 3.0 introduce una forma avanzata di concatenamento delle licenze, in cui una foglia è associata a una licenza principale, e solo la licenza principale è associata a un computer o a un dominio specifico. Leggi Concatenamento *licenze* avanzato in *Utilizzo di Adobe Access SDK per la protezione dei contenuti*.

* **Rotazione chiave:** Durante la creazione di pacchetti tipici, il contenuto viene cifrato utilizzando la chiave di crittografia dei contenuti (CEK) e il client ottiene una licenza contenente la CEK per utilizzare il contenuto. Quando la rotazione delle chiavi è abilitata, la chiave utilizzata per cifrare il contenuto può essere modificata in modo che la chiave venga utilizzata solo per cifrare una parte del contenuto. Leggi Rotazione ** chiave in *Utilizzo di Adobe Access SDK per la protezione dei contenuti*.

* **Licenze fuori banda:** Con Adobe Access è possibile implementare un flusso di lavoro in cui i client ottengono licenze pre-generate fuori banda, eliminando la necessità di distribuire un server licenze.
* **Supporto del dominio:** In alternativa al binding di una licenza con un dispositivo specifico, Adobe Access supporta il binding delle licenze a un dominio. Più dispositivi possono entrare a far parte di un dominio e ricevere un token di dominio che consente lo spostamento delle licenze tra dispositivi nel dominio. Leggi Registrazione ** dominio in *Utilizzo di Adobe Access SDK per la protezione dei contenuti*.

* **Cifratura parziale:** Specifica se tutti i fotogrammi, o solo un sottoinsieme di fotogrammi, devono essere codificati. Sono disponibili tre livelli di crittografia: bassa, media e alta. La riduzione del livello di cifratura potrebbe ridurre il sovraccarico della CPU sui computer di fascia inferiore.
* **Creazione di pacchetti di contenuti scollegati:** La creazione di pacchetti di contenuto non richiede una connessione di rete al server licenze. In questo modo è possibile garantire la sicurezza delle operazioni back-end limitando l&#39;esposizione di contenuti compressi non ancora protetti.
* **Controllo del ripristino dell&#39;orologio: **Adobe Access fornisce un calcolo sicuro e accurato del tempo necessario per rilevare il ripristino dell&#39;orologio sul computer client. In questo modo vengono applicati i diritti relativi all&#39;accesso ai contenuti per un periodo di tempo specifico e i consumatori non possono sovvertire i diritti di accesso modificando l&#39;ora del computer.
* **Individuazione**: Consente il binding del contenuto a un computer specifico.
* **Elenco di opzioni applicazione:** Consente al runtime client di garantire che il contenuto protetto venga riprodotto solo all&#39;interno di un&#39;applicazione SWF o AIR autorizzata.
* **Revoca dei client compromessi: **Il software client compromesso può essere revocato. Se il runtime Flash Player o Adobe AIR viene determinato come compromesso, il servizio può essere rifiutato a tali client fino a quando non effettuano l&#39;aggiornamento a una versione più recente e sicura del software client.
* **Criteri multipli per lo stesso file video: **Un singolo contenuto video può presentare più criteri incorporati durante la creazione del pacchetto. Quando si rilascia una licenza, il server licenze può decidere quale criterio utilizzare, consentendo a un distributore di contenuti di utilizzare lo stesso file protetto per diversi modelli aziendali (ad esempio noleggio e vendita elettronica).

