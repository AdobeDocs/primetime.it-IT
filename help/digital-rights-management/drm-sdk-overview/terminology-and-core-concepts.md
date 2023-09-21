---
title: Terminologia e concetti fondamentali
description: Terminologia e concetti fondamentali
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Terminologia e concetti fondamentali{#terminology-and-core-concepts}

In questo documento vengono utilizzati i termini e i concetti seguenti:

**Consumatore**

Il *consumer* è l’utente finale che scarica o invia in streaming i contenuti.

**Contenuto**

*Contenuto* è costituito da file audio o video digitali.

**Chiave crittografia contenuto**

Il *Chiave crittografia contenuto* (CEK) è una chiave di crittografia utilizzata per crittografare il contenuto.

**Proprietari del contenuto**

*Proprietari del contenuto* sono le entità aziendali proprietarie del copyright del contenuto. Si può trattare di studi cinematografici di grandi dimensioni o di piccoli produttori indipendenti di film o di altri contenuti audiovisivi.

**Packagers dei contenuti**

*Packagers dei contenuti* sono organizzazioni che creano pacchetti di contenuti da utilizzare con Adobe Primetime DRM. I proprietari o i distributori dei contenuti possono scegliere di creare un pacchetto dei propri contenuti o possono avvalersi dei servizi di terze parti per creare un pacchetto dei contenuti e distribuirlo elettronicamente tramite Internet.

**Certificato digitale**

*Certificati digitali* (denominati anche *certificati*) associare un&#39;entità, ad esempio un individuo, un&#39;organizzazione o un sistema, a una specifica coppia di chiavi pubblica e privata. I certificati digitali possono essere considerati credenziali elettroniche che verificano l’identità di un individuo, un sistema o un’organizzazione.

**Firma digitale**

A *firma digitale* associa l’identità dell’editore al contenuto pubblicato e fornisce un meccanismo per rilevare eventuali manomissioni. Gli algoritmi di firma digitale utilizzano funzioni di hash di crittografia e algoritmi di crittografia asimmetrici o con coppia di chiavi pubblica/privata. Alcune firme digitali sfruttano anche i certificati digitali e l&#39;infrastruttura a chiave pubblica (PKI) per associare le chiavi pubbliche alle identità dei proprietari o dei distributori di contenuti.

**Distributore**

*Distributori* (denominati anche *distributori di contenuti* o* retailer*) sono entità aziendali che garantiscono i diritti di distribuzione ai proprietari dei contenuti per pubblicarli e diffonderli ai consumatori. In alcuni casi, la stessa entità è sia il proprietario del contenuto che il distributore del contenuto.

**Metadati DRM**

Informazioni inviate dal client (Adobe ® Flash® Player, Adobe® AIR® Runtime e client Primetime) per identificare il contenuto richiesto.

**Licenza**

Una *licenza *è una struttura di dati che contiene una chiave crittografata utilizzata per decrittografare il contenuto associato a una policy. La licenza viene generata da Primetime DRM quando il consumatore richiede il contenuto ed è associata al computer del consumatore. Utilizzando una policy come riferimento, la licenza definisce i diritti disponibili per il consumatore che scarica i contenuti. Per visualizzare il contenuto, il consumatore deve ottenere una licenza.

**Acquisizione licenza**

*Acquisizione licenza* è il processo di acquisizione di una licenza che consente al consumatore di decrittografare e visualizzare il contenuto protetto in base a una serie di regole di utilizzo. L’acquisizione della licenza si verifica quando un client invia informazioni che identificano il contenuto richiesto (il *Metadati DRM*) e il certificato del computer (che identifica il computer del consumatore) al server licenze (vedere di seguito).

**Server licenze**

Il * License Server *può essere integrato nei sistemi di fatturazione e autenticazione del distributore o del provider di servizi e può contenere una logica di business per verificare che il consumatore che richiede il contenuto protetto sia autorizzato a visualizzarlo. Se l’utente è autorizzato ad accedere al contenuto, il server licenze rilascia una licenza che consente al client di runtime di decrittografare e riprodurre il contenuto in base ai criteri e ai diritti associati all’account del consumatore.

È necessario creare e distribuire un server licenze utilizzando l’SDK DRM di Primetime.

**Policy**

A *policy* è un contenitore per le regole di utilizzo che determinano il modo in cui i consumatori possono utilizzare il contenuto protetto. I criteri vengono definiti indipendentemente dal contenuto protetto. Un criterio non applica diritti finché non è associato al contenuto tramite la licenza. Una policy elenca il set di regole di utilizzo, ovvero le autorizzazioni o i &quot;diritti&quot; che i consumatori hanno sul contenuto che acquistano. Ad esempio, i proprietari dei contenuti possono creare una policy che garantisca che i contenuti protetti siano accessibili solo dai consumatori per un periodo di tempo specifico. Questo criterio viene quindi applicato a tutto il contenuto per il quale il proprietario del contenuto desidera applicare questa restrizione.

I criteri vengono creati utilizzando Primetime DRM SDK.

**Contenuto protetto**

*Contenuto protetto* (denominati anche *contenuto impacchettato*) fa riferimento a contenuti video che sono stati crittografati con l’SDK Primetime DRM o altri strumenti supportati.

**Rivenditori**

Vedi la voce per *distributori* in questa sezione.
