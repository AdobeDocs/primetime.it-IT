---
title: Terminologia e concetti fondamentali
description: Terminologia e concetti fondamentali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Terminologia e concetti di base {#terminology-and-core-concepts}

In questo documento vengono utilizzati i seguenti termini e concetti:

**Consumatore**

Il *consumer* è l&#39;utente finale che scarica o invia in streaming i contenuti.

**Contenuto**

** Il contenuto è costituito da file audio o video digitali.

**Chiave di crittografia del contenuto**

La *Chiave di crittografia del contenuto* (CEK) è una chiave di crittografia utilizzata per crittografare il contenuto.

**Proprietari dei contenuti**

*I* proprietari dei contenuti sono le entità aziendali proprietarie dei diritti d&#39;autore sui contenuti. Possono essere grandi studi cinematografici, o piccoli produttori indipendenti di film o di altri contenuti audiovisivi.

**Pacchetti di contenuti**

*I pacchetti* di contenuti sono organizzazioni che creano pacchetti di contenuti da utilizzare con Adobe Access. I proprietari dei contenuti o i distributori possono scegliere di creare un pacchetto dei propri contenuti o possono inserire i servizi di terzi per creare pacchetti dei contenuti e distribuirli elettronicamente tramite Internet.

**Certificato digitale**

*I certificati digitali*  (denominati anche  *certificati*) associano un’entità, ad esempio una singola, organizzazione o sistema, a una coppia di chiavi pubblica e privata specifica. I certificati digitali possono essere considerati credenziali elettroniche che verificano l&#39;identità di una persona, di un sistema o di un&#39;organizzazione.

**Firma digitale**

Una *firma digitale* associa l&#39;identità dell&#39;editore al contenuto pubblicato e fornisce un meccanismo per rilevare le manomissioni. Gli algoritmi di firma digitale utilizzano funzioni hash di crittografia e algoritmi di cifratura asimmetrici (o a chiave pubblica/privata). Alcune firme digitali sfruttano inoltre i certificati digitali e l’infrastruttura a chiave pubblica (PKI) per associare le chiavi pubbliche alle identità dei proprietari o distributori di contenuti.

**Distributore**

*I distributori*  (anche denominati  ** distributori di contenuti o* rivenditori*) sono entità aziendali che garantiscono i diritti di distribuzione ai proprietari dei contenuti per pubblicare e diffondere i contenuti ai consumatori. In alcuni casi, la stessa entità è sia il proprietario del contenuto che il distributore di contenuti.

**Metadati DRM**

Informazioni inviate dal client (ovvero Adobe® Flash® Player, runtime Adobe® AIR® e client Primetime) per identificare il contenuto richiesto.

**Licenza**

Una *licenza *è una struttura di dati che contiene una chiave crittografata utilizzata per decrittografare il contenuto associato a un criterio. La licenza viene generata da Adobe Access quando il consumatore richiede il contenuto ed è associata al computer del consumatore. Utilizzando un criterio come riferimento, la licenza definisce i diritti disponibili per il consumatore che scarica il contenuto. Per visualizzare il contenuto, il consumatore deve ottenere una licenza.

**Acquisizione licenza**

*L’* acquisizione di licenze è il processo di acquisizione di una licenza che consente al consumatore di decrittografare e visualizzare il contenuto protetto in base a una serie di regole di utilizzo. L&#39;acquisizione della licenza si verifica quando un client invia al server licenze informazioni che identificano il contenuto richiesto (i *metadati DRM*) e il certificato del computer (che identifica il computer del consumatore) (vedi sotto).

**Server licenze**

Il* License Server *può essere integrato nei sistemi di fatturazione e autenticazione del distributore o del fornitore di servizi e può contenere logica di business per verificare che il consumatore che richiede contenuto protetto sia autorizzato a visualizzare il contenuto. Se l’utente è autorizzato ad accedere al contenuto, License Server rilascia una licenza che consente al client runtime di decrittografare e riprodurre il contenuto in base ai criteri e ai diritti associati all’account del consumatore.

È necessario creare e distribuire un server licenze utilizzando Adobe Access SDK.

**Criterio**

Un *policy* è un contenitore per le regole di utilizzo che determinano come i consumatori possono utilizzare i contenuti protetti. I criteri sono definiti indipendentemente dal contenuto protetto. Un criterio non applica i diritti finché non è associato al contenuto tramite la licenza. Un criterio elenca l’insieme di regole di utilizzo, ovvero le autorizzazioni o i &quot;diritti&quot; che i consumatori hanno per i contenuti che acquisiscono. Ad esempio, i proprietari dei contenuti possono creare un criterio che garantisca che i contenuti protetti siano accessibili solo dai consumatori per un periodo di tempo specifico. Questa policy viene quindi applicata a tutti i contenuti per i quali il proprietario del contenuto desidera applicare questa restrizione.

I criteri vengono creati utilizzando Adobe Access SDK.

**Contenuto protetto**

*Il contenuto*  protetto (detto anche contenuto  *incluso nel pacchetto*) si riferisce al contenuto video FLV e F4V che è stato crittografato utilizzando Adobe Access SDK o altri strumenti supportati.

**Rivenditori**

Vedi la voce relativa a *distributori* precedente in questa sezione.
