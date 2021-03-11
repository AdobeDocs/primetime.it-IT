---
title: Preferenze del pacchetto
description: Preferenze del pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Preferenze del pacchetto {#packager-preferences}

Questa scheda contiene le impostazioni necessarie per il contenuto del pacchetto. Nella tabella seguente sono descritte le seguenti preferenze:

| Preferenza | Descrizione |
|--- |--- |
| Certificato di trasporto server licenze | Il certificato di trasporto del server, rilasciato dall&#39;Adobe. Questo certificato viene utilizzato per proteggere le comunicazioni tra il client e il server licenze. Il file deve trovarsi nella directory delle risorse. |
| Abilita HSM | Specifica se i certificati e le credenziali vengono archiviati in un HSM. In tal caso, le preferenze relative ai certificati e alle credenziali verranno disattivate e sarà necessario specificare le proprietà nella scheda HSM. |
| Opzioni chiave di crittografia | Specifica in che modo la chiave di crittografia del contenuto viene crittografata al momento della creazione del pacchetto |
| Certificato del server licenze | Certificato del server licenze, rilasciato dall’Adobe. Il file deve trovarsi nella directory delle risorse. Il CEK viene crittografato con la chiave pubblica del server licenze. Solo i titolari della chiave privata del server licenze possono decrittografare la CEK. |
| Credenziali Packager | Credenziale del packager, rilasciata dall&#39;Adobe. Questo file viene utilizzato per firmare i metadati durante la creazione del pacchetto. |
| Nome file | Il file `PKCS#12` ( .pfx) contenente il certificato e la chiave privata. Il file deve trovarsi nella directory delle risorse. |
| Password file | Password per file .pfx |
| Proprietà cartella osservata globale | Specifica le impostazioni comuni a tutte le cartelle controllate configurate nel server. |
| Intervallo di controllo in millisecondi | Specifica la frequenza con cui le cartelle controllate devono verificare la presenza di nuovi contenuti da includere nel pacchetto. Il server esegue l&#39;iterazione di tutte le cartelle controllate configurate e quindi dorme per questo periodo di tempo. |
| Suffisso nome file di output | Specifica un&#39;estensione di file da aggiungere ai file di output. Ad esempio, se si specifica .out e il file di input è video.flv, il file di output sarà video.out.flv. |
| File di input di backup | Specifica se salvare una copia del contenuto originale. Se questa opzione non è selezionata, il file originale verrà eliminato dopo il completamento del pacchetto. |
| Nome della sottocartella di backup di input | Se è selezionata l’opzione File di input di backup, specifica una cartella in cui verranno salvati i file di input. Questa opzione specifica un nome di cartella relativo alla directory di input Cartella controllata. Se la cartella non esiste, verrà creata durante la creazione del pacchetto. |
| Sovrascrivi file di output esistenti | Specifica se il file di output può essere sovrascritto se esiste già un file con lo stesso nome. Se questa opzione non è selezionata e il file di output esiste già, l&#39;elaborazione del file di input verrà ignorata. |
