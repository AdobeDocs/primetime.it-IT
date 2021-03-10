---
title: Aggiornare il file WAR del server licenze
description: Aggiornare il file WAR del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Aggiornare il file WAR del server licenze{#update-the-license-server-war-file}

Per supportare i client che sono stati personalizzati tramite un server On Premises Individualization, è necessario aggiornare la radice del trust del certificato del server licenze per includere la credenziale CA di Individualization appena acquisita. Uno script Python ( [!DNL addIndivCert.py]) è incluso nella cartella [!DNL update_license_server] .

Per aggiornare il server licenze, effettuare le seguenti operazioni:

1. Crea una copia dei file WAR da aggiornare (esempi: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Assicurati che i file WAR siano sbloccati e che le relative autorizzazioni siano impostate in modo che possano essere modificate.
1. Esegui lo script [!DNL addIndivCert.py] Python per aggiornare i file WAR del server licenze.

   Gli input per lo script sono i seguenti:

   * `cert`: File PKCS12 contenente il certificato CA per l’individuazione delle persone
   * `war`: File WAR da aggiornare

   Il file di output è un file WAR aggiornato.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

I file WAR saranno modificati in posizione. Se necessario, è possibile modificare lo script Python in base alle esigenze specifiche. Dopo aver eseguito gli aggiornamenti, è possibile distribuire normalmente i file WAR.
