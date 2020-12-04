---
description: 'null'
seo-description: 'null'
seo-title: Configurare il database del server licenze
title: Configurare il database del server licenze
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Configurare il database del server licenze{#set-up-the-license-server-database}

Il server licenze di implementazione di riferimento richiede un database che supporti quanto segue:

* Autenticazione utente
* Regole aziendali dimostrative del modello di utilizzo
* Conversione metadati
* Supporto del dominio

L&#39;acquisizione anonima della licenza non richiede l&#39;esecuzione del database.

>[!NOTE]
>
>Questa procedura si applica solo a Microsoft Windows. Per altri sistemi operativi, consultate la documentazione del sistema operativo in uso o la documentazione di MySQL.

Per eseguire il server licenze, è necessario installare e configurare MySQL:

1. Sul DVD, accedete alla cartella [!DNL Third Party\MySQL\Installer\5.1] e avviate il programma di installazione.
1. Completare l&#39;installazione di MySQL.
1. Selezionare **[!UICONTROL Configure MySQL Server Now]** per avviare la procedura guidata di configurazione.
1. Fino alla quinta schermata, usate le impostazioni predefinite o selezionate impostazioni specifiche per il test.
1. Nella quinta schermata, selezionate **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e immettete il numero massimo di connessioni consentite.
1. Annotate la password principale.
1. Per reinstallare MySQL, se è necessario avviare il server in un secondo momento, completare i seguenti passaggi:
   1. Eliminare la cartella *unità di sistema:*.

      Questa cartella si trova in [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Eliminare la vecchia cartella di installazione di MySQL.

      Ad esempio, *unità di sistema:*, che si trova in [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Per installare MySQL JDBC Driver 5.1.7, copiate il file [!DNL mysql-connector-java-5.1.7-bin.jar] nella cartella [!DNL Third Party\MySQL\Installer\5.1] del DVD nella directory [!DNL ...\Tomcat6.0\lib] del server Tomcat.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 funziona con Tomcat 6.0. Le versioni precedenti di Tomcat non sono più supportate.

