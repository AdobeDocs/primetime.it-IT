---
title: Preferenze Packager
description: Preferenze Packager
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Preferenze Packager {#packager-preferences}

Questa scheda contiene le impostazioni necessarie per la creazione dei pacchetti di contenuto. Nella tabella seguente vengono descritte le preferenze riportate di seguito.

| Preferenza | Descrizione |
|--- |--- |
| Certificato trasporto server licenze | Il certificato di trasporto del server, rilasciato da Adobe. Questo certificato viene utilizzato per proteggere le comunicazioni tra il client e il server licenze. Il file deve trovarsi nella directory delle risorse. |
| Abilita HSM | Specifica se i certificati e le credenziali vengono archiviati in un HSM. In tal caso, le preferenze relative ai certificati e alle credenziali verranno disattivate e sarà necessario specificare le proprietà nella scheda HSM. |
| Opzioni di crittografia chiave | Specifica la modalità di crittografia della chiave di crittografia del contenuto al momento della creazione del pacchetto |
| Certificato server licenze | Il certificato del server licenze, rilasciato da Adobe. Il file deve trovarsi nella directory delle risorse. Il codice CEK è crittografato con la chiave pubblica del server licenze. Solo i titolari della chiave privata del server licenze possono decrittografare il codice CEK. |
| Credenziali Packager | Credenziali packager, emesse da Adobe. Questo file viene utilizzato per firmare i metadati durante la creazione del pacchetto. |
| Nome file | Il `PKCS#12` ( .pfx) file contenente il certificato e la chiave privata. Il file deve trovarsi nella directory delle risorse. |
| Password file | Password per il file PFX |
| Proprietà cartella controllata globale | Specifica le impostazioni comuni a tutte le cartelle controllate configurate nel server. |
| Intervallo di controllo in millisecondi | Specifica la frequenza con cui le cartelle controllate devono verificare la presenza di nuovi contenuti da includere nel pacchetto. Il server scorre tutte le cartelle controllate configurate, quindi sospende per questo periodo di tempo. |
| Suffisso nome file di output | Specifica un&#39;estensione di file da aggiungere ai file di output. Ad esempio, se si specifica l&#39;estensione out e il file di input è video.flv, il file di output sarà video.out.flv. |
| Backup dei file di input | Specifica se deve essere salvata una copia del contenuto originale. Se questa opzione non è selezionata, il file originale verrà eliminato al termine della creazione del pacchetto. |
| Nome sottocartella backup di input | Se l&#39;opzione Backup file di input è selezionata, specifica una cartella in cui verranno salvati i file di input. Questa opzione specifica un nome di cartella relativo alla directory di input della cartella controllata. Se la cartella non esiste, verrà creata durante la creazione del pacchetto. |
| Sovrascrivi file di output esistenti | Specifica se il file di output può essere sovrascritto se esiste già un file con lo stesso nome. Se questa opzione non è selezionata e il file di output esiste già, l’elaborazione del file di input verrà ignorata. |
