---
seo-title: Aggiornare il file WAR del server licenze
title: Aggiornare il file WAR del server licenze
uuid: 0cde53d6-185d-4bf2-84fc-0c31d17904a8
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# Aggiornare il file WAR del server licenze{#update-the-license-server-war-file}

Per supportare i client che sono stati individualizzati tramite un server On Premises Individualization, è necessario aggiornare il livello principale di affidabilità del certificato del server licenze per includere la credenziale Individualization CA appena acquisita. Uno script Python ( [!DNL addIndivCert.py]) è incluso nella [!DNL update_license_server] cartella.

Per aggiornare il server licenze, effettuate le seguenti operazioni:

1. Fare una copia dei file WAR da aggiornare (esempi: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Assicuratevi che i file WAR siano sbloccati e che le relative autorizzazioni siano impostate in modo che possano essere modificati.
1. Eseguire lo script [!DNL addIndivCert.py] Python per aggiornare i file WAR del server licenze.

   Gli input per lo script sono i seguenti:

   * `cert`: File PKCS12 contenente il certificato CA per l&#39;individuazione delle persone
   * `war`: File WAR da aggiornare
   Il file di output è un file WAR aggiornato.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

I file WAR saranno modificati in posizione. Se necessario, potete modificare lo script Python in base alle vostre esigenze specifiche. Dopo aver eseguito gli aggiornamenti, è possibile distribuire i file WAR normalmente.
