---
title: Configurare il database del server licenze
description: Configurare il database del server licenze
copied-description: true
exl-id: be6232b4-bf51-486f-9c85-ab6f6ec6d9bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Configurare il database del server licenze{#set-up-the-license-server-database}

Il server licenze di implementazione di riferimento richiede un database che supporti quanto segue:

* Autenticazione utente
* Regole aziendali dimostrative del modello di utilizzo
* Conversione metadati
* Supporto del dominio

L&#39;acquisizione anonima delle licenze non richiede l&#39;esecuzione del database.

>[!NOTE]
>
>Questa procedura è valida solo per Microsoft Windows. Per altri sistemi operativi, consultare la documentazione del sistema operativo in uso o fare riferimento alla documentazione MySQL.

Per eseguire il server licenze, è necessario installare e configurare MySQL:

1. Sul DVD, passare alla [!DNL Third Party\MySQL\Installer\5.1] e avviare il programma di installazione.
1. Completare l&#39;installazione di MySQL.
1. Seleziona **[!UICONTROL Configure MySQL Server Now]** per avviare la configurazione guidata.
1. Fino alla quinta schermata, utilizza le impostazioni predefinite o seleziona impostazioni specifiche per il test.
1. Nella quinta schermata, seleziona **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e inserisci il numero massimo di connessioni consentite.
1. Scrivere la password root.
1. Per reinstallare MySQL, se è necessario avviare il server in un secondo momento, effettuare le seguenti operazioni:
   1. Elimina *unità di sistema:* cartella.

      Questa cartella si trova in [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Elimina la cartella di installazione MySQL precedente.

      Ad esempio: *unità di sistema:*, che si trova in [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Per installare MySQL JDBC Driver 5.1.7, copiare [!DNL mysql-connector-java-5.1.7-bin.jar] file in [!DNL Third Party\MySQL\Installer\5.1] cartella sul DVD per [!DNL ...\Tomcat6.0\lib] sul server Tomcat.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 funziona con Tomcat 6.0. Le versioni precedenti di Tomcat non sono più supportate.
