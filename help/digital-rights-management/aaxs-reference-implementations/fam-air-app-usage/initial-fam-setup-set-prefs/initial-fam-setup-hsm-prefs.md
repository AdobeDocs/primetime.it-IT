---
seo-title: Preferenze HSM
title: Preferenze HSM
uuid: 1b97d582-d4b6-48cd-9c24-2d13493571e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Preferenze HSM {#hsm-preferences}

Le preferenze in questa scheda devono essere specificate solo se la casella di controllo **[!UICONTROL Enable HSM]** è selezionata nella scheda Packager. Nella tabella seguente sono descritte le seguenti preferenze:

| Preferenza | Descrizione |
|---|---|
| Nome file di configurazione Sun PKCS#11 | Percorso completo del file di configurazione del provider Sun PKCS#11. Per informazioni dettagliate sul contenuto di questo file di configurazione, consultate la guida di riferimento PKCS#11 Java sul sito Web di Sun. |
| Password partizione | La password per la partizione HSM specificata nel file di configurazione PKCS#11. |
| Alias certificato server licenze | Alias per  certificato del server licenze rilasciato dal Adobe memorizzato in HSM. Questo certificato viene utilizzato per cifrare il CEK durante la creazione del pacchetto. Specificate questo valore invece di *Certificato server licenze* nella scheda Packager. |
| Alias certificato trasporto server licenze | Alias per  certificato di trasporto server emesso dal Adobe memorizzato in HSM. Questo certificato è utilizzato per proteggere le comunicazioni tra il client e il server licenze. Specificate questo valore invece di *Certificato di trasporto server licenze* nella scheda Packager. |
| Alias credenziali Packager | Alias per  credenziale packager rilasciata dal Adobe (certificato e chiave privata) archiviata in HSM. Viene utilizzato per firmare i metadati durante la creazione del pacchetto. Specificate questo valore invece di *Credenziali Packager* nella scheda Packager. |
| Alias credenziali server licenze | Alias per  credenziale del server licenze rilasciata dal Adobe (certificato e chiave privata) memorizzato in HSM. Questa credenziale viene utilizzata per firmare gli elenchi degli aggiornamenti dei criteri. Specificate questo valore invece di *Credenziali server licenze* nella scheda Elenco aggiornamenti criteri. (Questo alias sarà probabilmente uguale a *Alias certificato server licenze*.) |

