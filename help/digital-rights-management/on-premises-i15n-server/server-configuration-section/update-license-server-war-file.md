---
title: Aggiornare il file WAR del server licenze
description: Aggiornare il file WAR del server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Aggiornare il file WAR del server licenze{#update-the-license-server-war-file}

Per supportare i client individualizzati tramite un server di personalizzazione locale, è necessario aggiornare la radice di attendibilità del certificato del server licenze in modo da includere le credenziali della CA di personalizzazione appena acquisite. Uno script Python ( [!DNL addIndivCert.py]) è incluso nel [!DNL update_license_server] cartella.

Per aggiornare il server licenze, procedere come segue:

1. Creare una copia dei file WAR da aggiornare (esempi: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Assicurati che i file WAR siano sbloccati e che le relative autorizzazioni siano impostate in modo che possano essere modificati.
1. Esegui il [!DNL addIndivCert.py] Script Python per aggiornare i file WAR del server licenze.

   Gli input per lo script sono i seguenti:

   * `cert`: file PKCS12 contenente il certificato CA di Personalizzazione
   * `war`: file WAR da aggiornare

   Il file di output è un file WAR aggiornato.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

I file WAR verranno modificati. Se necessario, puoi modificare lo script Python in base alle tue esigenze. Dopo aver eseguito gli aggiornamenti, è possibile distribuire i file WAR normalmente.
