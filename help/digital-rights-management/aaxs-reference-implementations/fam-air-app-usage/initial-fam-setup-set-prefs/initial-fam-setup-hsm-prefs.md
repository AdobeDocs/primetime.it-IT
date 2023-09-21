---
title: Preferenze HSM
description: Preferenze HSM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Preferenze HSM {#hsm-preferences}

Le preferenze in questa scheda devono essere specificate solo se **[!UICONTROL Enable HSM]** nella scheda Packager. Nella tabella seguente vengono descritte le preferenze riportate di seguito.

| Preferenza | Descrizione |
|---|---|
| Nome file di configurazione Sun PKCS#11 | Percorso completo del file di configurazione del provider Sun PKCS#11. Per informazioni dettagliate sul contenuto di questo file di configurazione, consultare la Guida di riferimento di Java PKCS#11 sul sito Web di Sun. |
| Password partizione | Password per la partizione HSM specificata nel file di configurazione PKCS#11. |
| Alias certificato server licenze | Alias per il certificato del server di licenze rilasciato dagli Adobi archiviato in HSM. Questo certificato viene utilizzato per crittografare il CEK durante la creazione del pacchetto. Specifica questo invece di *Certificato server licenze* nella scheda Packager. |
| Alias certificato trasporto server licenze | Alias per il certificato di trasporto del server rilasciato dagli Adobi archiviato in HSM. Questo certificato viene utilizzato per proteggere le comunicazioni tra il client e il server licenze. Specifica questo invece di *Certificato trasporto server licenze* nella scheda Packager. |
| Alias credenziali Packager | Alias per le credenziali packager emesse dall&#39;Adobe (certificato e chiave privata) memorizzate in HSM. Viene utilizzato per firmare i metadati durante la creazione del pacchetto. Specifica questo invece di *Credenziali Packager* nella scheda Packager. |
| Alias credenziali server licenze | Alias per le credenziali del server licenze rilasciate dall&#39;Adobe (certificato e chiave privata) memorizzate in HSM. Queste credenziali vengono utilizzate per firmare gli elenchi di aggiornamento dei criteri. Specifica questo invece di *Credenziali server licenze* nella scheda Elenco aggiornamenti criteri. (Questo alias sarà probabilmente lo stesso di *Alias certificato server licenze*.) |
