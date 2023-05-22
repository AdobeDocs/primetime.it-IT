---
title: Scaricare e configurare i prerequisiti software
description: Il processo di installazione è semplice. Se sul sistema è già installato JDK, puoi saltare questo passaggio, ma tieni presente che JDK, Eclipse IDE e il sistema operativo devono essere compatibili.
exl-id: c2884a55-4f5e-4da8-807d-633625d7fef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Scaricare e configurare i prerequisiti software {#download-and-configure-prerequisite-software}

1. Scarica JDK da [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   Il processo di installazione è semplice. Se sul sistema è già installato JDK, puoi saltare questo passaggio, ma tieni presente che JDK, Eclipse IDE e il sistema operativo devono essere compatibili.
1. Scarica l’IDE Eclipse per sviluppatori Java da [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Dopo aver decompresso il pacchetto, puoi eseguire direttamente Eclipse. Nessun programma di installazione.
1. Scarica il bundle ADT SDK per Android da [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Questo pacchetto include Eclipse. Se nel sistema è già installato Eclipse, puoi scaricare gli strumenti SDK per la tua piattaforma da [!UICONTROL Use An Existing IDE] sezione.

   Decomprimi e installa in una posizione che ricorderai. Sarà necessario fare riferimento a questo in un passaggio successivo.
1. Configura l&#39;SDK per Android.
   1. Aprire un terminale (in Mac OS X) o un prompt dei comandi (in Windows).
   1. Passa alla directory in cui hai scaricato/decompresso l’SDK Android.
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

      In Windows, se Eclipse non si avvia e il problema segnalato è che Eclipse non riesce a trovare un file Java necessario, prova quanto segue:

      * aggiungi `-vm C:\[path to your JDK bin]\javaw.exe` al tuo [!DNL eclipse.ini] file.
   1. Seleziona  **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. Clic **[!UICONTROL Add...]**.
   1. Invio `Android` per il nome.
   1. Invio `https://dl-ssl.google.com/android/eclipse/` per **[!UICONTROL Work with]** collegamento.
   1. Clic **[!UICONTROL OK]**.

      Dovresti visualizzare una finestra di dialogo simile alla seguente:

      ![](assets/available_software.jpg)

   1. Seleziona i pacchetti risultanti (quelli in Strumenti per sviluppatori e plug-in NDK) e fai clic su **[!UICONTROL Next]**.

      Questo consente di scaricare gli strumenti di sviluppo Android (ADT).
   1. Al termine del download, riavvia Eclipse.

   L’SDK per Android è ora installato. 1. Configura Eclipse in modo che possa trovare l’SDK Android e utilizzarlo come risorsa.
   1. Apri Eclipse.
   1. Seleziona  **[!UICONTROL Window]** > **[!UICONTROL Preferences]** su Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** su Mac OS X.
   1. Seleziona la **[!UICONTROL Android]** scheda.
   1. Passa alla posizione dell’SDK per Android.
   1. Clic **[!UICONTROL Apply]**.

      ![Risultato passaggio](assets/ss2.jpg)
