---
title: Preferenze HSM
description: Preferenze HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Preferenze HSM {#hsm-preferences}

Le preferenze in questa scheda devono essere specificate solo se la casella di controllo **[!UICONTROL Enable HSM]** è selezionata nella scheda Packager. Nella tabella seguente sono descritte le seguenti preferenze:

| Preferenza | Descrizione |
|---|---|
| Sun PKCS#11 Nome file di configurazione | Percorso completo del file di configurazione del provider Sun PKCS#11. Per informazioni dettagliate sul contenuto di questo file di configurazione, consultate la Java PKCS#11 Reference Guide sul sito web Sun. |
| Password partizione | Password per la partizione HSM specificata nel file di configurazione PKCS#11. |
| Alias certificato server licenze | Alias per il certificato del server licenze rilasciato da Adobe memorizzato in HSM. Questo certificato viene utilizzato per crittografare il CEK durante il packaging. Specifica questo al posto di *Certificato del server licenze* nella scheda Packager. |
| Alias certificato di trasporto server licenze | Alias per il certificato di trasporto server rilasciato da Adobe memorizzato in HSM. Questo certificato viene utilizzato per proteggere le comunicazioni tra il client e il server licenze. Specifica questo al posto di *Certificato di trasporto del server licenze* nella scheda Packager. |
| Alias credenziali del pacchetto | Alias per le credenziali del packager emesse da Adobi (certificato e chiave privata) memorizzate in HSM. Viene utilizzato per firmare i metadati durante la creazione del pacchetto. Specifica questo invece di *Credenziali Packager* nella scheda Packager. |
| Alias credenziali server licenze | Alias per le credenziali del server licenze rilasciate in Adobe (certificato e chiave privata) memorizzate in HSM. Questa credenziale viene utilizzata per firmare gli elenchi degli aggiornamenti dei criteri. Specifica questo al posto di *Credenziali server licenze* nella scheda Elenco aggiornamenti criteri . (Questo alias sarà probabilmente lo stesso di *Alias del certificato del server licenze*.) |

