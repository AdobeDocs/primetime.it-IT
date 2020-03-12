---
seo-title: Configurazione del database e configurazione dell'origine dati JNDI
title: Configurazione del database e configurazione dell'origine dati JNDI
uuid: 1326523f-c053-4169-a934-1b2d3907b1f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurazione del database e configurazione dell&#39;origine dati JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

Il server licenze di implementazione di riferimento richiede un database che supporti le seguenti funzionalità:

* Autenticazione utente
* Regole aziendali dimostrative del modello di utilizzo
* Conversione metadati
* Supporto del dominio

L&#39;acquisizione anonima della licenza non richiede l&#39;esecuzione di un database.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Le istruzioni riportate in questa sezione sono relative alla piattaforma Microsoft Windows. Per altri sistemi operativi, consultate la documentazione del sistema operativo in uso o la documentazione di MySQL.

Per eseguire il server licenze, è necessario installare e configurare MySQL 5.1.34:

1. Eseguire il programma di installazione MySQL (disponibile nella terza cartella Party\MySQL\Installer\5.1 sul DVD).
1. Al termine della procedura di installazione, verificare **[!UICONTROL Configure MySQL Server Now]** di avviare la procedura guidata di configurazione. Utilizzate le impostazioni predefinite o selezionate impostazioni specifiche a scopo di test, con l&#39;eccezione che nella quinta schermata è necessario selezionare **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** immettere il numero massimo di connessioni consentito.

1. Prendete nota della password principale.
1. Se è necessario reinstallare MySQL, eseguire la procedura seguente per evitare problemi all&#39;avvio successivo del server:

   * Eliminare l’unità *del sistema di cartelle:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Eliminate la vecchia cartella di installazione di MySQL: ad esempio, unità *di sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Successivamente, sarà necessario installare il driver MySQL JDBC 5.1.7. A questo scopo, copiate [!DNL mysql-connector-java-5.1.7-bin.jar] (nella [!DNL Third Party\MySQL\Installer\5.1] cartella del DVD) nella directory Tomcat Server lib: [!DNL ...\Tomcat6.0\lib].

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>MySQL JDBC Driver 5.1.7 funziona con Tomcat 6.0. Le versioni precedenti di Tomcat non sono supportate.

Configurate il database di esempio configurando lo schema del database e compilando il database con dati di esempio. Per eseguire questa operazione, effettuare le seguenti operazioni:

1. Vai a **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. Dopo aver digitato la password, eseguire il seguente script SQL per aggiungere l&#39;account utente `dbuser` per stabilire una connessione tramite un&#39;applicazione Web e creare lo schema del database (assicurarsi che alla fine non sia presente &quot;;&quot;. Premere Invio.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Modificare lo script che compila i dati di esempio nelle tabelle per includere i dati a scopo di test: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Esegui questo script per compilare i dati come hai fatto al passaggio 2.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La prima volta che si esegue lo [!DNL CreateSampleDB.sql] script si verificherà l&#39;errore seguente:

*ERRORE 1396 (HY000): Operazione UTENTE DROP non riuscita per la query &#39;dbuser&#39;@&#39;localhost&#39; OK. 0 righe interessate (0,00 sec).*

Questo errore può essere ignorato. Questa operazione viene eseguita solo la prima volta che si esegue lo script.

A questo punto sarà necessario configurare Database Connection Pooling (DBCP). DBCP utilizza il pool di connessioni del database Jakarta-Commons. Un TestDB origine dati JNDI è configurato per sfruttare il pool di connessioni del server applicazione. Per modificare la connessione al database in modo che punti a un server MySQL che non si trova in localhost, modificare il [!DNL META-INF\context.xml] file (che specifica il percorso, il nome utente e la password del database del server licenze) che si trova in [!DNL flashaccess.war], oppure modificare [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] e ricreare il file WAR utilizzando i file aggiornati. Per modificare uno di questi parametri, modificare la [!DNL context.xml] posizione nella directory WebContent e utilizzare lo script Ant per ricreare il file WAR. Per ottimizzare il database, modificare le impostazioni dell&#39;origine dati JNDI in questo file.

Se esegui il debug del progetto di implementazione di riferimento in Eclipse, devi aggiungere `$CATALINA_HOME\lib\tomcat-dbcp.jar` alla configurazione di esecuzione/debug. Questo passaggio non è richiesto se esegui il [!DNL flashaccess.war] file su un server Tomcat 6.0 standalone.
