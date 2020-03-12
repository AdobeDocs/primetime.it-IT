---
seo-title: Preferenze HSM
title: Preferenze HSM
uuid: 1b97d582-d4b6-48cd-9c24-2d13493571e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Preferenze HSM {#hsm-preferences}

Le preferenze in questa scheda devono essere specificate solo se la **[!UICONTROL Enable HSM]** casella di controllo è selezionata nella scheda Packager. Nella tabella seguente sono descritte le seguenti preferenze:

| Preferenza | Descrizione |
|---|---|
| Nome file di configurazione Sun PKCS#11 | Percorso completo del file di configurazione del provider Sun PKCS#11. Per informazioni dettagliate sul contenuto di questo file di configurazione, consultate la guida di riferimento PKCS#11 Java sul sito Web di Sun. |
| Password partizione | La password per la partizione HSM specificata nel file di configurazione PKCS#11. |
| Alias certificato server licenze | Alias per il certificato del server licenze rilasciato da Adobe memorizzato in HSM. Questo certificato viene utilizzato per cifrare il CEK durante la creazione del pacchetto. Specificate questa opzione invece del certificato *del server di* licenze nella scheda Packager. |
| Alias certificato trasporto server licenze | Alias per il certificato di trasporto server emesso da Adobe memorizzato in HSM. Questo certificato è utilizzato per proteggere le comunicazioni tra il client e il server licenze. Specificate questa opzione invece del certificato *di trasporto server* licenze nella scheda Packager. |
| Alias credenziali Packager | Alias per le credenziali del packager emesso da Adobe (certificato e chiave privata) archiviate in HSM. Viene utilizzato per firmare i metadati durante la creazione del pacchetto. Specificate questa opzione invece di Credenziali ** Packager nella scheda Packager. |
| Alias credenziali server licenze | Alias per le credenziali del server di licenze emesso da Adobe (certificato e chiave privata) archiviate in HSM. Questa credenziale viene utilizzata per firmare gli elenchi degli aggiornamenti dei criteri. Specificate questa opzione invece di Credenziali *server* licenze nella scheda Elenco aggiornamenti criteri. Questo alias sarà probabilmente lo stesso dell&#39;alias *del certificato del server di* licenze. |

