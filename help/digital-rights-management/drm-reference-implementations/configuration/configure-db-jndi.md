---
title: Configurare il database del server licenze
description: Configurare il database del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Configura il database del server licenze{#configure-the-license-server-database}

Per configurare il database di esempio impostando lo schema del database e compilando il database con dati di esempio:

1. Visualizza la riga di comando MySQL.

   **Su Windows -** Fai clic su   **[!UICONTROL Window's Start Menu]** >  **[!UICONTROL MySQL]** >  **[!UICONTROL MySQL Server 5.1]** >  **[!UICONTROL MySQL Command Line Client]**

   **Su Linux, ecc.** - Tipo  `MySQL`.

1. Esegui il seguente script SQL:

   mysql> origine &quot;`"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Questo script aggiunge l&#39;account utente `dbuser`, stabilisce una connessione tramite un&#39;applicazione Web e crea uno schema di database.

   >[!NOTE]
   >
   >Assicurati che alla fine dello script non sia presente un punto e virgola ( `;`).

1. Modifica lo script `PopulateSampleDB.sql` che compila i dati di esempio nelle tabelle in modo da includere i dati per il test.

   Questo script si trova nella cartella `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` .
1. Esegui lo script [!DNL PopulateSampleDB] per compilare i dati come hai fatto al passaggio 2.

   >[!NOTE]
   >
   >La prima volta che esegui lo script [!DNL CreateSampleDB.sql] si verifica il seguente errore:

   È possibile ignorare questo errore in tutta sicurezza. Viene eseguito solo la prima volta che si esegue questo script.

È necessario configurare Database Connection Pooling (DBCP), che utilizza il pool di connessioni al database Jakarta-Commons. Un Datasource TestDB JNDI è configurato per sfruttare questo pool di connessioni server applicazioni. Per modificare la connessione al database in modo che punti a un server MySQL che non si trova su localhost, modificare uno dei file seguenti:

* Il file [!DNL META-INF\context.xml], che specifica il percorso, il nome utente e la password del database del server licenze presente nel file [!DNL flashaccess.war].

* Il file `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml`.

e ricreare il file WAR utilizzando i file aggiornati.

Per modificare uno di questi parametri, modifica il file [!DNL context.xml] nella directory [!DNL WebContent] e utilizza lo script Ant per ricreare il file WAR. Per ottimizzare il database, modificare le impostazioni dell&#39;origine dati JNDI in questo file.

Se esegui il debug del progetto di implementazione di riferimento in Eclipse, aggiungi `$CATALINA_HOME\lib\tomcat-dbcp.jar` alla configurazione di esecuzione/debug.

>[!NOTE]
>
>Se esegui il file [!DNL flashaccess.war] su un server Tomcat 6.0 autonomo, questo passaggio non è necessario.

