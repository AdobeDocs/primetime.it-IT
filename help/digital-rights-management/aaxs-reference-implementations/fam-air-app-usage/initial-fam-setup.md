---
title: Configurazione iniziale di Flash Access Manager
description: Configurazione iniziale di Flash Access Manager
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Configurazione iniziale di Flash Access Manager {#initial-flash-access-manager-setup}

Per impostare Gestione Flash Access, attenersi alla procedura descritta di seguito.

1. Distribuire il server Packager. Questo server dovrebbe essere disponibile solo per gli utenti all&#39;interno del firewall (non distribuire il software su un computer pubblico). Per ulteriori informazioni sulla distribuzione del server, vedere [Distribuzione del server licenze e del packager delle cartelle controllate](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Copia [!DNL flashaccess-packager.war] nella cartella webapps di Tomcat.
   * Copia [!DNL flashaccess-refimpl-packager.properties] dalle risorse a una posizione nel percorso di classe.
   * Avvia il server. Verranno visualizzati alcuni errori a causa di problemi nel file delle proprietà. Ciò è previsto in quanto le proprietà non sono ancora state compilate.

1. Installare l&#39;applicazione AIR di Flash Access Manager avviando [!DNL .air] (richiede AIR 1.5 o versione successiva).
1. Avvia l&#39;applicazione AIR di Flash Access Manager.

   Se il server è in esecuzione in un percorso diverso da `https://localhost:8080*`, vengono visualizzati errori che indicano che l&#39;applicazione non è in grado di connettersi al server. Chiudere la finestra di dialogo di errore e immettere l&#39;URL corretto per l&#39;URL del server Packager nella scheda Preferenze. Se il server è in esecuzione nell&#39;URL specificato e il file delle proprietà si trova nel percorso di classe, nella schermata Preferenze verranno inseriti i valori nel file delle proprietà. Dopo aver impostato l&#39;URL del server di creazione pacchetti, l&#39;applicazione AIR ricorda questa impostazione e non sarà necessario immetterla al successivo avvio dell&#39;applicazione.
1. Inserisci i valori nella scheda Preferenze e fai clic su **[!UICONTROL Save]**.
1. Se desideri utilizzare le Cartelle controllate, dovrai riavviare il server per ripristinare gli errori visualizzati nel passaggio 3. Se le preferenze sono configurate correttamente, all&#39;avvio non dovrebbero comparire errori.
