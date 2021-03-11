---
title: Configurazione del database e configurazione dell'origine dati JNDI
description: Configurazione del database e configurazione dell'origine dati JNDI
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Configurazione del database e configurazione dell&#39;origine dati JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

Il server licenze di implementazione di riferimento richiede un database per supportare le seguenti funzionalità:

* Autenticazione utente
* Regole aziendali dimostrative del modello di utilizzo
* Conversione dei metadati
* Supporto del dominio

L&#39;acquisizione con licenza anonima non richiede l&#39;esecuzione di un database.

>[!NOTE]
>
>Le istruzioni contenute in questa sezione sono per la piattaforma Microsoft Windows. Per altri sistemi operativi, consultare la documentazione relativa al sistema operativo in uso o consultare la documentazione di MySQL.

Per eseguire il server licenze, è necessario installare e configurare MySQL 5.1.34:

1. Eseguire il programma di installazione di MySQL (che si trova nella terza cartella Party\MySQL\Installer\5.1 sul DVD).
1. Al termine della procedura di installazione, selezionare **[!UICONTROL Configure MySQL Server Now]** per avviare la procedura guidata di configurazione. Utilizzare le impostazioni predefinite o selezionare impostazioni specifiche a scopo di test, con l&#39;eccezione che nella quinta schermata è necessario selezionare **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e immettere il numero massimo di connessioni consentite.

1. Prendi nota della password principale.
1. Se è necessario reinstallare MySQL, seguire questi passaggi per evitare problemi nell&#39;avvio successivo del server:

   * Elimina la cartella *unità di sistema:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Elimina la cartella di installazione di MySQL precedente: ad esempio, *unità di sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Successivamente, sarà necessario installare il driver JDBC MySQL 5.1.7. A questo scopo, copiare [!DNL mysql-connector-java-5.1.7-bin.jar] (nella cartella [!DNL Third Party\MySQL\Installer\5.1] sul DVD) nella directory lib Tomcat Server: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>Il driver JDBC MySQL 5.1.7 funziona con Tomcat 6.0. Le versioni precedenti di Tomcat non sono supportate.

Impostare il database di esempio impostando lo schema del database e compilando il database con dati di esempio. A questo scopo, esegui le seguenti operazioni:

1. Vai a **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. Dopo aver digitato la password, eseguire il seguente script SQL per aggiungere l&#39;account utente `dbuser` per stabilire una connessione tramite un&#39;applicazione Web e creare uno schema di database (assicurarsi che alla fine non vi sia &quot;;&quot;. Premere Invio.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Modificare lo script che popola i dati di esempio nelle tabelle per includere i dati a scopo di test: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Esegui questo script per compilare i dati come nel passaggio 2.

>[!NOTE]
>
>La prima volta che esegui lo script [!DNL CreateSampleDB.sql] riceverai il seguente errore:

*ERRORE 1396 (HY000): Operazione DROP USER non riuscita per la query &#39;dbuser&#39;@&#39;localhost&#39; OK, 0 righe interessate (0,00 sec).*

È possibile ignorare questo errore in tutta sicurezza. Questo accade solo la prima volta che esegui questo script.

A questo punto sarà necessario configurare Database Connection Pooling (DBCP). DBCP utilizza il pool di connessioni al database Jakarta-Commons. Un Datasource TestDB JNDI è configurato per sfruttare questo pool di connessioni server applicazioni. Per modificare la connessione al database in modo che punti a un server MySQL che non si trova su localhost, modificare il file [!DNL META-INF\context.xml] (che specifica il percorso, il nome utente e la password del database del server licenze) che si trova in [!DNL flashaccess.war] oppure modificare [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] e ricreare il file WAR utilizzando i file aggiornati. Per modificare uno di questi parametri, modificare il [!DNL context.xml] situato nella directory WebContent e utilizzare lo script Ant per ricreare il file WAR. Per ottimizzare il database, modificare le impostazioni dell&#39;origine dati JNDI in questo file.

Se esegui il debug del progetto di implementazione di riferimento in Eclipse, devi aggiungere `$CATALINA_HOME\lib\tomcat-dbcp.jar` alla configurazione di esecuzione/debug. Questo passaggio non è necessario se esegui il file [!DNL flashaccess.war] su un server Tomcat 6.0 autonomo.
