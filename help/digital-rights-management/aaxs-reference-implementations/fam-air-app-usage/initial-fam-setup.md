---
description: 'null'
seo-description: 'null'
seo-title: Configurazione iniziale di Flash Access Manager
title: Configurazione iniziale di Flash Access Manager
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurazione iniziale di Flash Access Manager {#initial-flash-access-manager-setup}

Per impostare Flash Access Manager, effettuate le seguenti operazioni:

1. Implementate il server Packager. Questo server dovrebbe essere disponibile solo per gli utenti all&#39;interno del firewall (non distribuire il software su un computer rivolto al pubblico). Per ulteriori informazioni sull&#39;implementazione del server, vedere [Distribuzione del server licenze e del packager](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)cartelle controllato.

   * Copia [!DNL flashaccess-packager.war] nella cartella delle app Web di Tomcat.
   * Copiare [!DNL flashaccess-refimpl-packager.properties] le risorse in una posizione nel percorso di classe.
   * Avviate il server. Verranno visualizzati alcuni errori a causa di problemi nel file delle proprietà; è previsto perché le proprietà non sono ancora state compilate.

1. Installate l’applicazione AIR Flash Access Manager avviando il [!DNL .air] file (richiede AIR 1.5 o versione successiva).
1. Avviate l’applicazione AIR Flash Access Manager.

   Se il server è in esecuzione in un altro [*!DNL https:// localhost:8080*], vengono visualizzati errori che indicano che l&#39;applicazione non è in grado di connettersi al server. Nella scheda Preferenze, chiudete la finestra di dialogo di errore e inserite l&#39;URL corretto per l&#39;URL del server Packager. Se il server è in esecuzione all&#39;URL specificato e il file delle proprietà si trova nel percorso di classe, nella schermata Preferenze verranno inseriti i valori nel file delle proprietà. Dopo aver impostato l&#39;URL del server del packager, l&#39;applicazione AIR ricorda questa impostazione e non sarà necessario immetterla al successivo avvio dell&#39;applicazione.
1. Compila i valori nella scheda Preferenze e fai clic su **[!UICONTROL Save]**.
1. Se si desidera utilizzare le cartelle esaminate, sarà necessario riavviare il server per recuperare gli errori che si sono verificati al punto 3. Se le preferenze sono configurate correttamente, durante l&#39;avvio non dovrebbero essere visualizzati errori.

