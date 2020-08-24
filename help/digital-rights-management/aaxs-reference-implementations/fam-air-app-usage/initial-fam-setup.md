---
description: 'null'
seo-description: 'null'
seo-title: Configurazione iniziale di Gestione Flash Access
title: Configurazione iniziale di Gestione Flash Access
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# Configurazione iniziale di Gestione Flash Access {#initial-flash-access-manager-setup}

Per configurare Gestione Flash Access, effettuate le seguenti operazioni:

1. Implementate il server Packager. Questo server dovrebbe essere disponibile solo per gli utenti all&#39;interno del firewall (non distribuire il software su un computer rivolto al pubblico). Per ulteriori informazioni sull&#39;implementazione del server, vedere [Distribuzione del server licenze e del packager](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)cartelle controllato.

   * Copia [!DNL flashaccess-packager.war] nella cartella delle app Web di Tomcat.
   * Copiare [!DNL flashaccess-refimpl-packager.properties] le risorse in una posizione nel percorso di classe.
   * Avviate il server. Verranno visualizzati alcuni errori a causa di problemi nel file delle proprietà; è previsto perché le proprietà non sono ancora state compilate.

1. Installate l&#39;applicazione AIR di Flash Access Manager avviando il [!DNL .air] file (richiede AIR 1.5 o versione successiva).
1. Avviate l&#39;applicazione AIR di Gestione Flash Access.

   Se il server è in esecuzione in un altro `https://localhost:8080*`, vengono visualizzati errori che indicano che l&#39;applicazione non è in grado di connettersi al server. Nella scheda Preferenze, chiudete la finestra di dialogo di errore e inserite l&#39;URL corretto per l&#39;URL del server Packager. Se il server è in esecuzione all&#39;URL specificato e il file delle proprietà si trova nel percorso di classe, nella schermata Preferenze verranno inseriti i valori nel file delle proprietà. Dopo aver impostato l&#39;URL del server del packager, l&#39;applicazione AIR ricorda questa impostazione e non sarà necessario immetterla al successivo avvio dell&#39;applicazione.
1. Compila i valori nella scheda Preferenze e fai clic su **[!UICONTROL Save]**.
1. Se si desidera utilizzare le cartelle esaminate, sarà necessario riavviare il server per recuperare gli errori che si sono verificati al punto 3. Se le preferenze sono configurate correttamente, durante l&#39;avvio non verrà visualizzato alcun errore.

