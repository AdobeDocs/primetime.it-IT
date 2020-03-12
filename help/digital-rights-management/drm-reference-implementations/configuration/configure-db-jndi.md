---
description: 'null'
seo-description: 'null'
seo-title: Configurare il database del server licenze
title: Configurare il database del server licenze
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurare il database del server licenze{#configure-the-license-server-database}

Per configurare il database di esempio configurando lo schema del database e compilando il database con dati di esempio:

1. Aprire la riga di comando MySQL.

   **In Windows -** Fare clic **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **Su Linux, ecc.** - Tipo `MySQL`.

1. Eseguire il seguente script SQL:

   mysql> origine &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Questo script aggiunge l&#39;account utente `dbuser`, stabilisce una connessione tramite un&#39;applicazione Web e crea uno schema del database.

   >[!NOTE]
   >
   >Verificare che alla fine dello script non sia presente un punto e virgola ( `;`).

1. Modificare lo `PopulateSampleDB.sql` script che compila i dati di esempio nelle tabelle per includere i dati per il test.

   Questo script si trova nella `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` cartella.
1. Eseguire lo [!DNL PopulateSampleDB] script per compilare i dati come nel passaggio 2.

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >La prima volta che si esegue lo [!DNL CreateSampleDB.sql] script si verifica l&#39;errore seguente:

   Questo errore può essere ignorato. Viene eseguito solo la prima volta che si esegue questo script.

È necessario configurare il Database Connection Pooling (DBCP), che utilizza il pool di connessioni del database Jakarta-Commons. Un TestDB origine dati JNDI è configurato per sfruttare il pool di connessioni del server applicazione. Per modificare la connessione al database in modo che punti a un server MySQL non presente nell&#39;host locale, modificare uno dei seguenti file:

* Il [!DNL META-INF\context.xml] file, che specifica il percorso, il nome utente e la password del database del server licenze che si trova nel [!DNL flashaccess.war] file.

* Il `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` file.

e ricreare il file WAR utilizzando i file aggiornati.

Per modificare uno di questi parametri, modificare il [!DNL context.xml] file nella [!DNL WebContent] directory e utilizzare lo script Ant per ricreare il file WAR. Per ottimizzare il database, modificare le impostazioni dell&#39;origine dati JNDI in questo file.

Se esegui il debug del progetto di implementazione di riferimento in Eclipse, aggiungi `$CATALINA_HOME\lib\tomcat-dbcp.jar` alla configurazione di esecuzione/debug.

>[!NOTE]
>
>Se esegui il [!DNL flashaccess.war] file su un server Tomcat 6.0 standalone, questo passaggio non è richiesto.

