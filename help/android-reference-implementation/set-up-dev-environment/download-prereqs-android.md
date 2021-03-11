---
title: Download e configurazione del software di prerequisiti
description: Il processo di installazione è semplice. Se nel sistema è già installato JDK, puoi saltare questo passaggio, ma tieni presente che JDK, Eclipse IDE e OS devono essere compatibili.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Scarica e configura il software prerequisito {#download-and-configure-prerequisite-software}

1. Scarica il JDK da [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   Il processo di installazione è semplice. Se nel sistema è già installato JDK, puoi saltare questo passaggio, ma tieni presente che JDK, Eclipse IDE e OS devono essere compatibili.
1. Scarica l&#39;IDE Eclipse per sviluppatori Java da [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Dopo aver decompresso il pacchetto, puoi eseguire direttamente Eclipse. Nessun programma di installazione.
1. Scarica il bundle ADT dell&#39;SDK per Android da [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Questo bundle include Eclipse. Se hai già installato Eclipse sul tuo sistema, puoi scaricare gli strumenti SDK per la tua piattaforma dalla sezione [!UICONTROL Use An Existing IDE] .

   Estrai e installa in una posizione che ricorderai. Sarà necessario fare riferimento a questo in un passaggio successivo.
1. Configura l&#39;SDK per Android.
   1. Apri un terminale (in Mac OS X) o un prompt dei comandi (in Windows).
   1. Vai alla directory in cui hai scaricato/decompresso l’SDK per Android.
   1. Vai alla cartella degli strumenti, che contiene un file denominato [!DNL android].
   1. Esegui i seguenti comandi:

      * Per Mac OS X/Unix:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * Per Windows:

         ```
         android update sdk --no-ui
         ```

         Questo processo richiede un po&#39; di tempo.

1. Configura Eclipse.
   1. Avvia Eclipse.

      In Windows, se Eclipse non si avvia e il problema segnalato è che Eclipse non è in grado di trovare un file Java richiesto, prova quanto segue:

      * aggiungi `-vm C:\[path to your JDK bin]\javaw.exe` al file [!DNL eclipse.ini].
   1. Seleziona **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. Clic **[!UICONTROL Add...]**.
   1. Immettere `Android` come nome.
   1. Immetti `https://dl-ssl.google.com/android/eclipse/` per il collegamento **[!UICONTROL Work with]**.
   1. Clic **[!UICONTROL OK]**.

      Viene visualizzata una finestra di dialogo simile a questa:

      ![](assets/available_software.jpg)

   1. Seleziona i pacchetti risultanti (quelli in Strumenti per sviluppatori e plugin NDK) e fai clic su **[!UICONTROL Next]**.

      Questo scarica gli strumenti di sviluppo Android (ADT).
   1. Al termine del download, riavvia Eclipse.

   L&#39;SDK per Android è ora installato. 1. Configura Eclipse in modo che possa trovare l&#39;SDK per Android e utilizzarlo come risorsa.
   1. Apri Eclipse.
   1. Selezionare **[!UICONTROL Window]** > **[!UICONTROL Preferences]** su Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** su Mac OS X.
   1. Seleziona la scheda **[!UICONTROL Android]** .
   1. Individua il percorso dell’SDK Android.
   1. Clic **[!UICONTROL Apply]**.

      ![Risultato del passaggio](assets/ss2.jpg)


