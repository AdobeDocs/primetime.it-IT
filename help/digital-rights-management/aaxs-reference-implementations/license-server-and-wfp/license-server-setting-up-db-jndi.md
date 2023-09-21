---
title: Configurazione del database e dell’origine dati JNDI
description: Configurazione del database e dell’origine dati JNDI
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Configurazione del database e dell’origine dati JNDI {#setting-up-the-database-and-configuring-the-jndi-datasource}

Il server licenze di implementazione di riferimento richiede un database per supportare le seguenti funzionalità:

* Autenticazione utente
* Regole aziendali dimostrative del modello di utilizzo
* Conversione metadati
* Supporto del dominio

L&#39;acquisizione di licenze anonime non richiede l&#39;esecuzione di un database.

>[!NOTE]
>
>Le istruzioni contenute in questa sezione si riferiscono alla piattaforma Microsoft Windows. Per altri sistemi operativi, consultare la documentazione del sistema operativo in uso o fare riferimento alla documentazione MySQL.

Per eseguire il server licenze, è necessario installare e configurare MySQL 5.1.34:

1. Eseguire il programma di installazione MySQL (disponibile nella terza cartella Party\MySQL\Installer\5.1 del DVD).
1. Al termine della procedura di installazione, controllare **[!UICONTROL Configure MySQL Server Now]** per avviare la configurazione guidata. Utilizza le impostazioni predefinite o seleziona impostazioni specifiche a scopo di test, con l’eccezione che nella quinta schermata devi selezionare **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e inserisci il numero massimo di connessioni consentite.

1. Prendere nota della password root.
1. Se è necessario reinstallare MySQL, eseguire la procedura seguente per evitare problemi nell&#39;avvio del server in seguito:

   * Elimina la cartella *unità di sistema:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Elimina la cartella di installazione MySQL precedente: ad esempio, *unità di sistema:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Sarà quindi necessario installare MySQL JDBC Driver 5.1.7. Per eseguire questa operazione, copia [!DNL mysql-connector-java-5.1.7-bin.jar] (disponibile nella sezione [!DNL Third Party\MySQL\Installer\5.1] sul DVD) nella directory della libreria di Tomcat Server: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC Driver 5.1.7 funziona con Tomcat 6.0. Le versioni precedenti di Tomcat non sono supportate.

Impostare il database di esempio impostando lo schema del database e popolandolo con dati di esempio. A questo scopo, effettua le seguenti operazioni:

1. Vai a  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. Dopo aver digitato la password, eseguire lo script SQL seguente per aggiungere l&#39;account utente `dbuser` per stabilire una connessione tramite un’applicazione web e creare uno schema di database (assicurati che non sia presente &quot;;&quot; alla fine. Premere Invio.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Modifica lo script che compila i dati di esempio nelle tabelle per includere i dati a scopo di test: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Esegui questo script per popolare i dati come hai fatto nel passaggio 2.

>[!NOTE]
>
>La prima volta che esegui [!DNL CreateSampleDB.sql] script verrà visualizzato il seguente errore:

*ERRORE 1396 (HY000): operazione DROP USER non riuscita per la query &#39;dbuser&#39;@&#39;localhost&#39; OK, 0 righe interessate (0,00 sec).*

Puoi ignorare questo errore. Questo accade solo la prima volta che esegui questo script.

A questo punto è necessario configurare il connection pooling del database (DBCP). DBCP utilizza il pool di connessioni al database Jakarta-Commons. Un database di origine dati JNDI TestDB è configurato per sfruttare questo pool di connessioni al server applicazioni. Per modificare la connessione al database in modo che punti a un server MySQL che non si trova su localhost, modificare il [!DNL META-INF\context.xml] file (che specifica la posizione, il nome utente e la password del database del server licenze) che si trova in [!DNL flashaccess.war], o modifica [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] e ricreare il file WAR utilizzando i file aggiornati. Per modificare uno di questi parametri, modificare il [!DNL context.xml] si trova nella directory WebContent e utilizza lo script Ant per ricreare il file WAR. Per ottimizzare il database, modificare le impostazioni dell&#39;origine dati JNDI in questo file.

Se esegui il debug del progetto di implementazione di riferimento in Eclipse, devi aggiungere `$CATALINA_HOME\lib\tomcat-dbcp.jar` alla configurazione di esecuzione/debug. Questo passaggio non è necessario se si esegue [!DNL flashaccess.war] su un server Tomcat 6.0 autonomo.
