---
description: 'null'
seo-description: 'null'
seo-title: Impostare il token XSTS nel lettore
title: Impostare il token XSTS nel lettore
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# Streaming su Xbox360 (facoltativo) {#streaming-to-xboc360}

Primetime DRM è disponibile sulla piattaforma Xbox360. Tuttavia, è supportato solo il caso di utilizzo dello streaming protetto, non l&#39;intera suite di diritti per i criteri DRM. I diritti dei criteri DRM non in streaming, ad esempio Gruppi di dominio dispositivo, non sono supportati. Xbox360 ignora i diritti non supportati quando si tenta di riprodurre il contenuto.

I diritti supportati per l&#39;informativa DRM di Primetime per Xbox sono:
* Protezione dell&#39;uscita digitale
* Data fine cache offline licenza
* Data inizio licenza
* Data fine licenza
* Durata della finestra di riproduzione (secondi)

Il contenuto potrebbe non dover essere reinserito in un pacchetto per lo streaming su Xbox360, se è già stato creato un pacchetto per un&#39;altra piattaforma Primetime, ad esempio iOS, Android o Desktop.

Un avvertimento con Xbox360 è che deve sempre raggiungere un server chiave ogni volta che un tag EXT-X-KEY viene rilevato nel M3U8. A differenza di iOS, in cui un&#39;impostazione DRM Policy (policy.requestKeyServer) causerà al lettore video iOS Primetime di recuperare la chiave di decrittazione AES da localhost, Xbox tenterà sempre di recuperare la chiave di decrittazione da un server di chiavi remoto. Non esiste alcun diritto di criterio DRM per indicare all&#39;app Xbox di recuperare la decrittazione AES
key from localhost. A causa di questo requisito, le voci EXT-X-KEY devono essere in M3U8 che punta all&#39;endpoint DRM di Primetime Cloud. Questo URL viene impostato tramite &lt;key_url> nel file di configurazione OfflinePackager.jar config_hls.xml.

Se desiderate creare un pacchetto di contenuto una volta e farlo scorrere a tutte le destinazioni Primetime, nonché configurare i dispositivi iOS per non recuperare una chiave da un server di chiavi remoto, potete creare un pacchetto di contenuto utilizzando un criterio DRM con la proprietà policy.requestKeyServer=false (ad esempio in policy_ios_localkeyserver.pol). I dispositivi iOS recupereranno la chiave AES localmente, mentre i dispositivi Xbox ignoreranno questa proprietà e si collegheranno al server chiavi DRM di Primetime Cloud
per una chiave di decrittazione.

>!Note
>
>Tutte le richieste Xbox360 devono utilizzare Autenticazione personalizzata/>Adesione. Questo perché sulla piattaforma Xbox360, Xbox Live >utilizza un token Xbox Secure Token Server (XSTS) per >scopi di autenticazione.
>Il server licenze DRM di Primetime Cloud utilizza il token XSTS per convalidare l&#39;integrità sia del dispositivo Xbox che dell&#39;utente che effettua > la richiesta di licenza. Tuttavia, la convalida del token XSTS richiede una chiave del fornitore privato Xbox Live del cliente, che Primetime Cloud DRM >non memorizza. Per questo motivo, quando Primetime Cloud DRM riceve una richiesta di licenza da un client Xbox 360, Primetime Cloud DRM >inoltrerà il token XSTS al back-end del cliente Primetime >Authentication/Entitlement server. Il server del cliente Primetime
>quindi analizzerà e convaliderà il token XSTS per verificare che sia stato >firmato utilizzando la chiave di pubblicazione dell&#39;applicazione del cliente.
>Per passare un token XSTS dal client Xbox360, imposta il token > in modo sincrono in risposta all&#39;evento MediaPlayer.RequestKeyAttribute >, descritto più dettagliatamente qui: **Impostare il token XSTS nel lettore.** Un esempio di server di autenticazione back-end/adesione >è incluso con la release software nella directory Autenticazione personalizzata >e Adesione.La convalida dei token XSTS viene descritta più avanti in questo dettaglio:  **Convalida token XSTS di Xbox Live.**


## Impostare il token XSTS nel lettore {#set-the-xsts-token-in-your-player}

In Xbox360, il token viene impostato in modo asincrono in risposta all&#39;evento `MediaPlayer.RequestKeyAttribute`.

Impostate il token XSTS.

L&#39;app di esempio fornita con il software mostra come impostare il token XSTS nel lettore. Segue il frammento di codice relativo al lettore di esempio:

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

## Convalida token Xbox Live XSTS {#xbox-live-xsts-token-validation}

Per le richieste XSTS, il campo `customerSpecificAuthToken` conterrà il token XSTS codificato Base64. Il codice di esempio `XSTSValidator` esamina il token decodificato Base64 per verificare l&#39;esistenza dell&#39;elemento `EncryptedAssertion`; tuttavia, potete utilizzare altri metodi per distinguere tra queste richieste e richieste non Xbox. Ad esempio, potete utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta ignorerà il criterio originale nei metadati DRM forniti con la richiesta della chiave Xbox. Solo un sottoinsieme delle funzionalità del criterio è supportato dal client Xbox e questi campi sono gli unici che ignoreranno il criterio originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decodifica e la convalida dei token. È necessario caricare le credenziali [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] in un archivio di chiavi in formato JKS, che vengono quindi fornite al server di adesione back-end come proprietà di sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l&#39;alias `xsts` e il certificato di convalida del token ha l&#39;alias `xsts-verify-cert`. È inoltre possibile ignorare tali impostazioni utilizzando le proprietà di sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` che non ha valore predefinito e che contiene la password dell&#39;archivio di chiavi. Le proprietà di sistema lette dal codice `XSTSValidator` sono riepilogate di seguito:

| Proprietà del sistema | Valore predefinito | Commento |
|---|---|---|
| xst-keystore | xsts.jks | Keystore di formato JKS utilizzato dal validatore. |
| xst-keystore-password |  | Password per l&#39;archivio chiavi |
| xst-alias | xste | Alias utilizzato per recuperare il tasto di decrittazione dall&#39;archivio di chiavi |
| xst-verify-cert-alias | xst-verify-cert | Alias utilizzato per recuperare il certificato di convalida dall&#39;archivio chiavi |

## Creare JKS per un validatore XSTS{#create-jks-for-an-xsts-validator}

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

   (dove `<alias>` è il nome alias del certificato privato scoperto al passaggio 1.)
1. Importa [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Inserire [!DNL xsts.jks] nella directory principale Tomcat e definire `-Dxsts-keystore-password=****` per Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] utilizzano password diverse, aggiornare la password `xsts` in `jks` per renderle uguali.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
