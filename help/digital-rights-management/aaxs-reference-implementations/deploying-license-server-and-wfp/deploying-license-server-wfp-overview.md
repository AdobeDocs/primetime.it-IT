---
seo-title: Panoramica sulla distribuzione del server licenze e del packager cartelle controllato
title: Panoramica sulla distribuzione del server licenze e del packager cartelle controllato
uuid: 4b71f2f4-f971-4382-ae41-171f7dfdfe21
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Panoramica sulla distribuzione del server licenze e del packager cartelle controllato {#deploying-the-license-server-and-watched-folder-packager-overview}

Copiare i file WAR del server licenze nella directory [!DNL webapps] di Tomcat. Se in precedenza avete distribuito il file WAR, potrebbe essere necessario eliminare manualmente le directory WAR non imballate ( [!DNL flashaccess], [!DNL edcws] e [!DNL flashaccess-packager] nella directory [!DNL webapps] di Tomcat). Per impedire a Tomcat di disfare i file WAR, modificate il file [!DNL server.xml] nella directory conf di Tomcat e impostate l&#39;attributo `unpackWARs` su `false`.

Il file delle proprietà ( [!DNL flashaccess-refimpl.properties]) deve trovarsi nel percorso di classe affinché il server possa caricare le proprietà. Copiate questo file in una directory e aggiornate il file con i valori appropriati. Modificate il file [!DNL catalina.properties] nella directory [!DNL conf] di Tomcat e aggiungete la directory contenente [!DNL flashaccess-refimpl.properties] alla proprietà `shared.loader`. Anche il file [!DNL log4j.xml] per la configurazione della registrazione deve trovarsi nel percorso di classe (vedere [!DNL resources\log4j.xml] ad esempio).

Il server di implementazione di riferimento utilizza diversi file di certificato, file di criteri e altre risorse. Tali file si trovano tutti in un’unica cartella di risorse. Per impostazione predefinita, la cartella delle risorse è [!DNL C:\flashaccess-server-resources], ma questo percorso può essere modificato in [!DNL flashaccess-refimpl.properties]. Prima di avviare il server, accertatevi di copiare tutte le risorse necessarie in questo percorso.

Per avviare Tomcat e il server licenze, eseguire `catalina.bat start` dalla directory [!DNL bin] di Tomcat.
