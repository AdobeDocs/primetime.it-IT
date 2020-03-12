---
uuid: 2d927ae8-4c4b-4b64-88b8-9c86430e226c
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Glossario {#glossary}

Termini utilizzati di frequente che richiedono una definizione speciale.

## Chiave di crittografia del contenuto {#content-encryption-key}

La chiave di crittografia del contenuto (CEK, content Encryption Key), generata da un&#39;utility, viene successivamente utilizzata da un packager per la preparazione del contenuto che deve essere protetto.
L&#39;utilità genera la chiave in esadecimale con una lunghezza di 16 byte.
Questa guida mostra, in note e messaggi di errore, file ed esempi di comandi, le seguenti varianti di nomi di parametri e nomi di valori per CEK:

* content key
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

I nomi dei file per CEK sono mostrati come:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

Il CEK stesso può essere memorizzato in un sistema di gestione chiave e cifrato. Questa guida fa riferimento all&#39;indice di storage come CEKSID CEK Storage ID. Il termine Chiave di crittografia (KEK) si riferisce alla chiave di crittografia di secondo livello e il termine `ek` fa riferimento al valore di tale crittografia.
Alcune chiamate utilizzano sia CEK che CEK Storage ID CEKSID, mentre il CEK recuperato dall’archivio deve corrispondere al CEK fornito nella chiamata.
Per HLS Offline con FairPlay, esiste anche un `persistentContentKey` che può essere impostato per scadere.

## ID archiviazione chiave di crittografia del contenuto {#content-encryption-key-storage-id}

L&#39;ID di archiviazione della chiave di crittografia dei contenuti (CEKSID) è un ID per il recupero di una chiave di crittografia dei contenuti da un sistema di gestione delle chiavi.

Il CEKSID è anche denominato
* ID chiave
* ID contenuto
* `&kid`

## Autenticazione cliente {#customer-authenticator}

Una chiave per l&#39;autenticazione nelle richieste all&#39;API di Expressplay. Le richieste possono includere richieste per i token.