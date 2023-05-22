---
description: La concessione di licenze è il meccanismo principale mediante il quale agli utenti viene consentita o negata la possibilità di riprodurre un contenuto video protetto. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decrittografare e riprodurre una parte specifica del contenuto crittografato del provider di contenuti.
title: Licenze
exl-id: 60aa3e77-f821-41b3-ba0e-1a2c05b2bb1a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Licenze{#licensing}

La concessione di licenze è il meccanismo principale mediante il quale agli utenti viene consentita o negata la possibilità di riprodurre un contenuto video protetto. A un utente legittimo (autorizzato) può essere rilasciata una licenza (una chiave) per decrittografare e riprodurre una parte specifica del contenuto crittografato del provider di contenuti.

Prima che l’app o la pagina web su un dispositivo di un utente finale possa riprodurre contenuti protetti da DRM, deve acquisire un token da un server di adesione o vetrina che tu, il cliente, utilizzi. Adobe fornisce un esempio di server di riferimento a questo scopo: [Server di riferimento: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

Il server autorizzato o storefront richiederà un token di licenza al server ExpressPlay interessato solo dopo aver verificato con i propri sistemi back-end se l&#39;utente specifico è autorizzato a guardare il contenuto richiesto. La risposta restituita dalla richiesta del token di licenza è un URL pronto all’uso per il server licenze oppure contiene l’URL in una struttura JSON, a seconda della soluzione DRM con cui stai lavorando.

>[!NOTE]
>
>Impossibile effettuare la richiesta del token di licenza dal client stesso:
>1. i diritti devono essere verificati in un ambiente attendibile; e
>1. L’autenticatore del cliente deve essere tenuto segreto.


1. Effettuare la richiesta del token di licenza.

   Per uno scenario di avvio rapido, in cui desideri semplicemente assicurarsi che i vari componenti coinvolti funzionino insieme, puoi utilizzare qualcosa di simile a [!DNL curl] per effettuare la richiesta del token di licenza (anziché avviare inizialmente un’app e testare le chiamate da lì). Ad esempio:

   * Widevine:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   Esempio di token di prova della linea wireless:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   La risposta di Widevine è una stringa URL &quot;pronta per l’uso&quot;.

   * PlayReady:

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   Token di prova PlayReady di esempio:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   La risposta PlayReady è un oggetto JSON, con elementi URL e token separati.

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   Esempio di token di test FairPlay:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   La risposta FairPlay è una stringa URL &quot;pronta per l’uso&quot;.
