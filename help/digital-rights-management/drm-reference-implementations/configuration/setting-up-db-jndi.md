---
title: Configurare il database del server licenze
description: Configurare il database del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Imposta il database del server licenze{#set-up-the-license-server-database}

Il server licenze di implementazione di riferimento richiede un database per supportare i seguenti elementi:

* Autenticazione utente
* Regole aziendali dimostrative del modello di utilizzo
* Conversione dei metadati
* Supporto del dominio

L&#39;acquisizione con licenza anonima non richiede l&#39;esecuzione del database.

>[!NOTE]
>
>Questa procedura si applica solo a Microsoft Windows. Per altri sistemi operativi, consultare la documentazione relativa al sistema operativo in uso o consultare la documentazione di MySQL.

Per eseguire il server licenze, è necessario installare e configurare MySQL:

1. Sul DVD, passare alla cartella [!DNL Third Party\MySQL\Installer\5.1] e avviare il programma di installazione.
1. Completare l&#39;installazione di MySQL.
1. Seleziona **[!UICONTROL Configure MySQL Server Now]** per avviare la procedura guidata di configurazione.
1. Fino alla quinta schermata, utilizza le impostazioni predefinite o seleziona le impostazioni specifiche per il test.
1. Nella quinta schermata, seleziona **[!UICONTROL Online Transaction Processing (OLTP)]** o **[!UICONTROL Manual Setting]** e immetti il numero massimo di connessioni consentite.
1. Annota la password principale.
1. Per reinstallare MySQL, se è necessario avviare il server in un secondo momento, completare i seguenti passaggi:
   1. Elimina la cartella *unità di sistema:*.

      Questa cartella si trova in [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Eliminare la cartella di installazione di MySQL precedente.

      Ad esempio, *unità di sistema:*, che si trova in [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Per installare il driver JDBC MySQL 5.1.7, copiare il file [!DNL mysql-connector-java-5.1.7-bin.jar] nella cartella [!DNL Third Party\MySQL\Installer\5.1] del DVD nella directory [!DNL ...\Tomcat6.0\lib] sul server Tomcat.

   >[!NOTE]
   >
   >Il driver JDBC MySQL 5.1.7 funziona con Tomcat 6.0. Le versioni precedenti di Tomcat non sono più supportate.

