---
title: Panoramica sulla distribuzione del server licenze e del gestore cartelle controllate
description: Panoramica sulla distribuzione del server licenze e del gestore cartelle controllate
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Panoramica sulla distribuzione del server licenze e del gestore cartelle controllate {#deploying-the-license-server-and-watched-folder-packager-overview}

Copiare i file WAR del server licenze nella directory [!DNL webapps] di Tomcat. Se in precedenza hai implementato il file WAR, potrebbe essere necessario eliminare manualmente le directory WAR decompresse ( [!DNL flashaccess], [!DNL edcws] e [!DNL flashaccess-packager] nella directory [!DNL webapps] di Tomcat. Per evitare che Tomcat scompili i file WAR, modifica il file [!DNL server.xml] nella directory conf di Tomcat e imposta l&#39;attributo `unpackWARs` su `false`.

Per caricare le proprietà, il file delle proprietà ( [!DNL flashaccess-refimpl.properties]) deve trovarsi nel percorso di classe del server. Copia questo file in una directory e aggiorna il file con i valori appropriati. Modifica il file [!DNL catalina.properties] nella directory [!DNL conf] di Tomcat e aggiungi la directory contenente [!DNL flashaccess-refimpl.properties] alla proprietà `shared.loader`. Anche il file [!DNL log4j.xml] per la configurazione della registrazione deve trovarsi nel percorso di classe (vedi [!DNL resources\log4j.xml] per un esempio).

Il server di implementazione di riferimento utilizza diversi file di certificato, file di criteri e altre risorse. Tali file si trovano tutti in una cartella di risorse. Per impostazione predefinita, la cartella delle risorse è [!DNL C:\flashaccess-server-resources], ma questo percorso può essere modificato in [!DNL flashaccess-refimpl.properties]. Prima di avviare il server, assicurati di copiare tutte le risorse necessarie in questa posizione.

Per avviare Tomcat e il server licenze, esegui `catalina.bat start` dalla directory [!DNL bin] di Tomcat.
