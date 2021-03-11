---
title: Imposta il token XSTS nel lettore
description: Imposta il token XSTS nel lettore
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---


# Streaming su Xbox360 (facoltativo) {#streaming-to-xboc360}

Primetime DRM è disponibile sulla piattaforma Xbox360. Tuttavia, è supportato solo il caso d’uso Streaming protetto, non la suite completa di diritti dei criteri DRM. I diritti dei criteri DRM non in streaming, come i gruppi di dominio del dispositivo, non sono supportati. Xbox360 ignora i diritti non supportati quando si tenta di riprodurre il contenuto.

I diritti supportati per i criteri DRM di Primetime per Xbox sono:
* Protezione dell&#39;uscita digitale
* Data fine memorizzazione in cache offline della licenza
* Data di inizio della licenza
* Data di fine della licenza
* Durata della finestra di riproduzione (secondi)

È possibile che non sia necessario reimpostare il contenuto per lo streaming su Xbox360, se è già stato compilato per un&#39;altra piattaforma Primetime, ad esempio iOS, Android o Desktop.

Un avvertimento con Xbox360 è che deve sempre raggiungere un server chiave ogni volta che si incontra un tag EXT-X-KEY in M3U8. A differenza di iOS, in cui un&#39;impostazione DRM Policy (policy.requiredKeyServer) farà sì che il lettore video iOS Primetime recuperi la chiave di decrittografia AES da localhost, Xbox tenterà sempre di recuperare la chiave di decrittografia da un server chiavi remoto. Non esiste alcun diritto di policy DRM per istruire l&#39;app Xbox per recuperare la decrittografia AES
chiave da localhost. A causa di questo requisito, le voci EXT-X-KEY devono essere nell’M3U8 che punta all’endpoint DRM di Primetime Cloud. Questo URL viene impostato tramite &lt;key_url> nel file di configurazione OfflinePackager.jar config_hls.xml.

Se desideri creare un pacchetto di contenuti una volta e farlo scorrere a tutte le destinazioni Primetime, nonché configurare i dispositivi iOS per non recuperare una chiave da un keyserver remoto, puoi creare un pacchetto di contenuti utilizzando un criterio DRM con la proprietà policy.requiredKeyServer=false (ad esempio in policy_ios_localkeyserver.pol). I dispositivi iOS recupereranno la chiave AES localmente, mentre i dispositivi Xbox ignoreranno questa proprietà e si rivolgeranno al server chiavi DRM di Primetime Cloud
per una chiave di decrittografia.

>!Nota
>
>Tutte le richieste Xbox360 devono utilizzare Autenticazione personalizzata/>Autorizzazione.Questo perché sulla piattaforma Xbox360, Xbox Live >utilizza un token XSTS (Secure Token Server) Xbox per scopi di autenticazione.
>Il server di licenza DRM di Primetime Cloud utilizza il token XSTS per >convalidare l&#39;integrità sia del dispositivo Xbox che dell&#39;utente che effettua >la richiesta di licenza. Tuttavia, la convalida del token XSTS richiede una chiave privata del cliente Xbox Live, che Primetime Cloud DRM >non memorizza. Per questo motivo, quando Primetime Cloud DRM riceve una richiesta di licenza da un client Xbox 360, Primetime Cloud DRM inoltrerà il token XSTS al server back-end del cliente Primetime >Authentication/Entitlement. Server del cliente Primetime
>analizzerà e convalida il token XSTS per verificare che sia stato >firmato utilizzando la chiave di pubblicazione dell’applicazione del cliente.
>Per passare un token XSTS dal client Xbox360, imposta il token >in modo sincrono in risposta all&#39;evento MediaPlayer.RequestKeyAttribute >event - descritto più dettagliatamente qui: **Imposta il token XSTS nel lettore.** Un esempio di server di autenticazione/autorizzazione back-end >è incluso con la versione del software nella directory di autenticazione personalizzata >e di abilitazione.La convalida dei token XSTS è discussa >in ulteriori dettagli qui:  **Convalida token XSTS di Xbox Live.**


## Imposta il token XSTS nel lettore {#set-the-xsts-token-in-your-player}

In Xbox360, imposti il token in modo asincrono in risposta all&#39;evento `MediaPlayer.RequestKeyAttribute` .

Imposta il token XSTS.

L’app di esempio abbinata al software mostra come impostare il token XSTS nel lettore. Di seguito è riportato lo snippet di codice relativo dal sample player:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## Convalida token XSTS Xbox Live {#xbox-live-xsts-token-validation}

Per le richieste XSTS, il campo `customerSpecificAuthToken` conterrà il token XSTS codificato Base64. Il codice di esempio `XSTSValidator` esamina il token decodificato Base64 per verificare l&#39;esistenza dell&#39;elemento `EncryptedAssertion`; tuttavia, puoi utilizzare altri metodi per distinguere tra queste richieste e richieste non Xbox. Ad esempio, puoi utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta ignorerà il criterio originale nei metadati DRM forniti con la richiesta di chiave Xbox. Solo un sottoinsieme di funzionalità dei criteri è supportato dal client Xbox e questi campi sono gli unici che ignoreranno il criterio originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decrittografia e la convalida dei token. È necessario caricare le credenziali [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] in un archivio chiavi in formato JKS, che viene quindi fornito al server di adesione back-end come proprietà del sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l’alias `xsts` e il certificato di convalida del token ha l’alias `xsts-verify-cert`. È inoltre possibile ignorarli utilizzando le proprietà del sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` che non ha un valore predefinito e che contiene la password del keystore. Le proprietà di sistema lette dal codice `XSTSValidator` sono riepilogate di seguito:

| Proprietà di sistema | Valore predefinito | Commento |
|---|---|---|
| xsts-keystore | xsts.jks | Archivio chiavi in formato JKS utilizzato dalla convalida. |
| xsts-keystore-password |  | Password per il keystore |
| xsts-alias | xsts | Alias utilizzato per recuperare la chiave di decrittografia dal keystore |
| xsts-verify-cert-alias | xsts-verify-cert | Alias utilizzato per recuperare il certificato di convalida dal keystore |

## Creare JKS per una convalida XSTS{#create-jks-for-an-xsts-validator}

1. Scopri il nome alias del certificato privato, che si trova nel file [!DNL .pfx] del partner.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Converti [!DNL .pfx] in [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (dove `<alias>` è il nome alias del certificato privato individuato al passaggio 1.)
1. Importa [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Inserisci [!DNL xsts.jks] nella home directory Tomcat e definisci `-Dxsts-keystore-password=****` per Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] utilizzano password diverse, aggiorna la password `xsts` in `jks` per renderle uguali.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
