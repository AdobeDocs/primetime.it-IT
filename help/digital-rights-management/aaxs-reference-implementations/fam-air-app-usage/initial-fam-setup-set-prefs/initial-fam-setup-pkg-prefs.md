---
seo-title: Preferenze Packager
title: Preferenze Packager
uuid: 3e9c971d-3a5f-4f3e-97e7-baab63b1f67f
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Preferenze Packager {#packager-preferences}

Questa scheda contiene le impostazioni necessarie per la creazione di pacchetti di contenuto. Nella tabella seguente sono descritte le seguenti preferenze:

| Preferenza | Descrizione |
|--- |--- |
| Certificato di trasporto server licenze | Il certificato di trasporto del server, rilasciato da Adobe. Questo certificato è utilizzato per proteggere le comunicazioni tra il client e il server licenze. Il file deve trovarsi nella directory delle risorse. |
| Abilita HSM | Specifica se i certificati e le credenziali vengono memorizzati in un HSM. In tal caso, le preferenze relative ai certificati e alle credenziali verranno disattivate e sarà necessario specificare le proprietà nella scheda HSM. |
| Opzioni crittografia chiave | Specifica in che modo la chiave di crittografia del contenuto viene cifrata al momento della creazione del pacchetto |
| Certificato server licenze | Certificato server licenze, rilasciato da Adobe. Il file deve trovarsi nella directory delle risorse. Il CEK è crittografato con la chiave pubblica del server licenze. Solo i titolari della chiave privata del server licenze possono decrittografare la CEK. |
| Credenziali Packager | La credenziale del packager, emessa da Adobe. Questo file viene utilizzato per firmare i metadati durante la creazione del pacchetto. |
| Nome file | Il file `PKCS#12` (.pfx) contenente il certificato e la chiave privata. Il file deve trovarsi nella directory delle risorse. |
| Password file | Password per il file .pfx |
| Proprietà globali cartella esaminata | Specifica le impostazioni comuni a tutte le cartelle esaminate configurate sul server. |
| Intervallo controllo in millisecondi | Specifica la frequenza con cui le cartelle esaminate devono verificare la presenza di nuovi contenuti da includere nel pacchetto. Il server esegue un&#39;iterazione in tutte le cartelle esaminate configurate e quindi rimane inattivo per questo periodo di tempo. |
| Suffisso nome file di output | Specifica un&#39;estensione di file da aggiungere ai file di output. Ad esempio, se si specifica .out e il file di input è video.flv, il file di output sarà video.out.flv. |
| Backup dei file di input | Specifica se salvare una copia del contenuto originale. Se questa opzione non è selezionata, il file originale verrà eliminato al termine del pacchetto. |
| Nome sottocartella di backup | Se l&#39;opzione Backup dei file di input è selezionata, specifica una cartella in cui verranno salvati i file di input. Questa opzione specifica un nome di cartella relativo alla directory di input della cartella esaminata. Se la cartella non esiste, verrà creata durante la creazione del pacchetto. |
| Sovrascrivi file di output esistenti | Specifica se il file di output può essere sovrascritto se esiste già un file con lo stesso nome. Se questa opzione non è selezionata e il file di output esiste già, l&#39;elaborazione del file di input verrà ignorata. |
