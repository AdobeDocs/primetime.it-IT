---
title: Configurazione iniziale di Flash Access Manager
description: Configurazione iniziale di Flash Access Manager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Configurazione iniziale di Flash Access Manager {#initial-flash-access-manager-setup}

Per configurare Gestione Flash Access, attenersi alla procedura descritta di seguito.

1. Distribuire il server Packager. Questo server dovrebbe essere disponibile solo per gli utenti all&#39;interno del firewall (non distribuire questo software su un computer rivolto al pubblico). Per ulteriori informazioni sulla distribuzione del server, consulta [Distribuzione del server licenze e del gestore cartelle controllate](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Copia [!DNL flashaccess-packager.war] nella cartella Web apps di Tomcat.
   * Copia [!DNL flashaccess-refimpl-packager.properties] dalle risorse in una posizione nel percorso di classe.
   * Avvia il server. Verranno visualizzati alcuni errori a causa di problemi nel file delle proprietà; questo è previsto perché le proprietà non sono state ancora compilate.

1. Installa l&#39;applicazione AIR Flash Access Manager avviando il file [!DNL .air] (richiede AIR 1.5 o superiore).
1. Avvia l’applicazione AIR Flash Access Manager.

   Se il server è in esecuzione in un punto diverso da `https://localhost:8080*`, vengono visualizzati errori che indicano che l&#39;applicazione non può connettersi al server. Ignora la finestra di dialogo dell&#39;errore e compila l&#39;URL corretto per l&#39;URL del server Packager nella scheda Preferenze. Se il server è in esecuzione nell&#39;URL specificato e il file delle proprietà si trova nel percorso di classe, nella schermata Preferenze verranno inseriti i valori nel file delle proprietà. Dopo aver impostato l&#39;URL del server del packager, l&#39;applicazione AIR ricorda questa impostazione e non sarà necessario inserirla al successivo avvio dell&#39;applicazione.
1. Inserisci i valori nella scheda Preferenze e fai clic su **[!UICONTROL Save]**.
1. Se si desidera utilizzare le Cartelle controllate, è necessario riavviare il server per recuperare gli errori visualizzati nel passaggio 3. Se le preferenze sono configurate correttamente, non dovrebbe essere visualizzato alcun errore durante l&#39;avvio.

