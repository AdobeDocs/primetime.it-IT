---
seo-title: Terminologia e concetti fondamentali
title: Terminologia e concetti fondamentali
uuid: 89a9e4b0-f5e1-4dc2-9cf8-0c8d7e9b7d62
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Terminologia e concetti fondamentali {#terminology-and-core-concepts}

In questo documento vengono utilizzati i seguenti termini e concetti:

**Consumer**

Il *consumatore* è l&#39;utente finale che scarica o invia in streaming il contenuto.

**Contenuto**

*Il contenuto* è costituito da file audio o video digitali.

**Chiave di crittografia del contenuto**

La chiave *di crittografia* del contenuto (CEK) è una chiave di crittografia utilizzata per cifrare il contenuto.

**Proprietari di contenuti**

*I proprietari* dei contenuti sono le entità aziendali proprietarie dei diritti d&#39;autore sui contenuti. Possono essere studi cinematografici di grandi dimensioni o piccoli produttori indipendenti di film o altri contenuti audiovisivi.

**Pacchetti di contenuti**

*I pacchetti* di contenuti sono organizzazioni che creano pacchetti di contenuti da utilizzare con Adobe Access. I proprietari dei contenuti o i distributori possono scegliere di creare pacchetti di contenuti personalizzati, oppure possono includere i servizi di terzi per creare pacchetti di contenuti e distribuirli elettronicamente tramite Internet.

**Certificato digitale**

*I certificati* digitali (denominati anche *certificati*) associano un&#39;entità, ad esempio un singolo, un&#39;organizzazione o un sistema, a una coppia di chiavi pubblica e privata specifica. I certificati digitali possono essere considerati come credenziali elettroniche per la verifica dell&#39;identità di un singolo, sistema o organizzazione.

**Firma digitale**

Una firma ** digitale vincola l&#39;identità dell&#39;editore al contenuto pubblicato e fornisce un meccanismo per rilevare eventuali manomissioni. Gli algoritmi di firma digitale utilizzano funzioni hash crittografiche e algoritmi di cifratura asimmetrici (o coppia di chiavi pubblica/privata). Alcune firme digitali sfruttano inoltre i certificati digitali e l&#39;infrastruttura a chiave pubblica (PKI) per legare le chiavi pubbliche alle identità dei proprietari o distributori di contenuti.

**Distributore**

*I distributori* (denominati anche distributori *di* contenuti o* rivenditori al dettaglio*) sono entità aziendali che garantiscono i diritti di distribuzione ai proprietari dei contenuti per pubblicare e divulgare i contenuti ai consumatori. In alcuni casi, la stessa entità è sia il proprietario del contenuto che il distributore di contenuti.

**Metadati DRM**

Informazioni inviate dal client (ovvero Adobe® Flash® Player, runtime Adobe® AIR® e client Primetime) per identificare il contenuto richiesto.

**Licenza**

Una *licenza *è una struttura di dati che contiene una chiave crittografata utilizzata per decifrare il contenuto associato a un criterio. La licenza viene generata da Adobe Access quando il consumatore richiede contenuto ed è associato al computer del consumatore. Utilizzando un criterio come riferimento, la licenza definisce i diritti disponibili per il consumatore che scarica il contenuto. Per visualizzare il contenuto, il consumatore deve ottenere una licenza.

**Acquisizione licenza**

*L&#39;acquisizione* della licenza è il processo di acquisizione di una licenza che consente al consumatore di decifrare e visualizzare il contenuto protetto in base a un insieme di regole di utilizzo. L&#39;acquisizione della licenza si verifica quando un client invia al server licenze informazioni che identificano il contenuto richiesto (i metadati ** DRM) e il certificato del computer (che identificano il computer del consumatore) (vedi sotto).

**Server licenze**

Il* License Server *può essere integrato nei sistemi di fatturazione e autenticazione del distributore o del fornitore di servizi e può contenere logica aziendale per verificare che il consumatore che richiede contenuto protetto sia autorizzato a visualizzare il contenuto. Se l&#39;utente è autorizzato ad accedere al contenuto, il server licenze rilascia una licenza che consente al client runtime di decifrare e riprodurre il contenuto in base al criterio e ai diritti associati all&#39;account del consumatore.

È necessario creare e distribuire un server licenze tramite l&#39;SDK di Adobe Access.

**Policy**

Un *criterio* è un contenitore per le regole di utilizzo che determinano in che modo i consumatori possono utilizzare il contenuto protetto. I criteri vengono definiti indipendentemente dal contenuto protetto. Un criterio non applica i diritti finché non viene associato al contenuto tramite la licenza. Un criterio elenca l&#39;insieme di regole di utilizzo, ossia le autorizzazioni o i &quot;diritti&quot; che i consumatori hanno per il contenuto acquisito. Ad esempio, i proprietari dei contenuti possono creare un criterio che garantisca che i contenuti protetti siano accessibili solo ai consumatori per un periodo di tempo specifico. Tale criterio viene quindi applicato a tutto il contenuto per il quale il proprietario del contenuto desidera applicare questa restrizione.

I criteri vengono creati utilizzando Adobe Access SDK.

**Contenuto protetto**

*Per contenuto* protetto (altrimenti denominato contenuto ** incluso nel pacchetto) si intende il contenuto video FLV e F4V cifrato mediante l’SDK di Adobe Access o altri strumenti supportati.

**Rivenditori**

Vedi la voce relativa ai *distributori* precedente in questa sezione.
