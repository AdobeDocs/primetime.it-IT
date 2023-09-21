---
title: Glossario
description: Termini utilizzati di frequente che richiedono una definizione speciale.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Glossario {#glossary}

Termini utilizzati di frequente che richiedono una definizione speciale.

## Chiave crittografia contenuto {#content-encryption-key}

La chiave di crittografia del contenuto (CEK), generata da un&#39;utility, viene successivamente utilizzata da un responsabile del pacchetto di contenuti nella preparazione dei contenuti che devono essere protetti.
L&#39;utility genera la chiave esadecimale con una lunghezza di 16 byte.
In questa guida vengono illustrate, nelle note e negli esempi di messaggi di errore, file e comandi, le seguenti varianti di nomi di parametri e di valori per il CEK:

* chiave contenuto
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

I nomi di file per un CEK sono visualizzati come:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

Il CEK può essere archiviato in un sistema di gestione delle chiavi e crittografato. Questa guida fa riferimento all’indice di archiviazione come CEK Storage ID CEKSID. Il termine chiave di crittografia (KEK) si riferisce alla chiave di crittografia di secondo livello e al termine `ek` fa riferimento al valore di tale crittografia.
Alcune chiamate utilizzano sia l’ID di archiviazione CEK che l’ID di archiviazione CEKSID e il CEK recuperato dall’archiviazione deve corrispondere al CEK fornito nella chiamata.
Per HLS Offline con FairPlay, è disponibile anche un `persistentContentKey` che può essere impostato per scadere.

## ID archiviazione chiave di crittografia contenuto {#content-encryption-key-storage-id}

L&#39;ID di archiviazione della chiave di crittografia del contenuto (CEKSID) è un ID per il recupero di una chiave di crittografia del contenuto da un sistema di gestione delle chiavi.

Il CEKSID è anche indicato come
* ID chiave
* ID contenuto
* `&kid`

## Autenticatore del cliente {#customer-authenticator}

Chiave per l’autenticazione nelle richieste all’API di Expressplay. Le richieste possono includere richieste di token.
