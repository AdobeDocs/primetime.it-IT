---
title: Glossario
description: Termini utilizzati di frequente che richiedono una definizione speciale.
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Glossario {#glossary}

Termini utilizzati di frequente che richiedono una definizione speciale.

## Chiave di crittografia dei contenuti {#content-encryption-key}

La chiave di crittografia del contenuto (CEK), generata da un&#39;utilità, viene successivamente utilizzata da un content packager per la preparazione del contenuto che deve essere protetto.
L&#39;utilità genera la chiave in esadecimale con una lunghezza di 16 byte.
Questa guida mostra, in note e messaggi di errore, file ed esempi di comando, le seguenti varianti di nomi di parametri e nomi di valori per CEK:

* content key
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

I nomi dei file per un CEK vengono visualizzati come:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

Il CEK stesso può essere memorizzato in un sistema di gestione delle chiavi e cifrato. Questa guida fa riferimento all&#39;indice di archiviazione come CEK Storage ID CEKSID. Il termine Chiave di crittografia (KEK) fa riferimento alla chiave di crittografia di secondo livello e il termine `ek` fa riferimento al valore di tale crittografia.
Alcune chiamate utilizzano sia il CEK che il CEK Storage ID CEKSID e il CEK recuperato dall&#39;archiviazione deve corrispondere al CEK fornito nella chiamata.
Per HLS Offline con FairPlay, esiste anche un `persistentContentKey` che può essere impostato per scadere.

## ID archiviazione chiave di crittografia del contenuto {#content-encryption-key-storage-id}

L’ID di archiviazione della chiave di crittografia del contenuto (CEKSID) è un ID per il recupero di una chiave di crittografia del contenuto da un sistema di gestione delle chiavi.

Il CEKSID è anche indicato come
* ID chiave
* ID contenuto
* `&kid`

## Utente autenticatore {#customer-authenticator}

Una chiave per l’autenticazione nelle richieste all’API di Expressplay. Le richieste possono includere richieste di token.
