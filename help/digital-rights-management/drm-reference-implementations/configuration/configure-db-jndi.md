---
title: Configurare il database del server licenze
description: Configurare il database del server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Configurare il database del server licenze{#configure-the-license-server-database}

Per configurare il database di esempio impostando lo schema del database e popolando il database con dati di esempio:

1. Visualizzare la riga di comando MySQL.

   **Su Windows -** Clic  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **Su Linux, ecc.** - Tipo `MySQL`.

1. Esegui il seguente script SQL:

   mysql> origine &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Questo script aggiunge l’account utente `dbuser`, stabilisce una connessione tramite un&#39;applicazione web e crea uno schema di database.

   >[!NOTE]
   >
   >Verificare che non sia presente il punto e virgola ( `;`) alla fine dello script.

1. Modifica il `PopulateSampleDB.sql` script che compila i dati di esempio nelle tabelle per includere i dati per il test.

   Questo script si trova in `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` cartella.
1. Esegui il [!DNL PopulateSampleDB] script per compilare i dati come nel passaggio 2.

   >[!NOTE]
   >
   >La prima volta che esegui [!DNL CreateSampleDB.sql] script si verifica il seguente errore:

   Puoi ignorare questo errore. Si verifica solo la prima volta che si esegue questo script.

È necessario configurare il DBCP (Database Connection Pooling) che utilizza il pool di connessioni al database Jakarta-Commons. Un database di origine dati JNDI TestDB è configurato per sfruttare questo pool di connessioni al server applicazioni. Per modificare la connessione al database in modo che punti a un server MySQL che non si trova su localhost, modificare uno dei file seguenti:

* Il [!DNL META-INF\context.xml] file, che specifica la posizione, il nome utente e la password del database del server licenze presente in [!DNL flashaccess.war] file.

* Il `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` file.

e ricreare il file WAR utilizzando i file aggiornati.

Per modificare uno di questi parametri, modificare il [!DNL context.xml] file in [!DNL WebContent] e utilizzare lo script Ant per ricreare il file WAR. Per ottimizzare il database, modificare le impostazioni dell&#39;origine dati JNDI in questo file.

Se esegui il debug del progetto di implementazione di riferimento in Eclipse, aggiungi `$CATALINA_HOME\lib\tomcat-dbcp.jar` alla configurazione di esecuzione/debug.

>[!NOTE]
>
>Se si esegue [!DNL flashaccess.war] su un server Tomcat 6.0 standalone, questo passaggio non è necessario.
