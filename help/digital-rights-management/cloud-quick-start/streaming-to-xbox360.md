---
title: Imposta il token XSTS nel lettore
description: Imposta il token XSTS nel lettore
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Streaming su Xbox360 (opzionale) {#streaming-to-xboc360}

Primetime DRM è disponibile sulla piattaforma Xbox360. Tuttavia, è supportato solo il caso di utilizzo di Streaming protetto, non la suite completa di diritti dei criteri DRM. I diritti dei criteri DRM non in streaming, ad esempio Gruppi di dominio dei dispositivi, non sono supportati. Xbox360 ignora i diritti non supportati quando si tenta di riprodurre contenuto.

I diritti supportati per i criteri DRM di Primetime per Xbox sono:
* Protezione dell&#39;uscita digitale
* Data di fine della memorizzazione in cache offline della licenza
* Data di inizio licenza
* Data di fine licenza
* Durata intervallo di riproduzione (secondi)

Il contenuto potrebbe non dover essere ricompilato per lo streaming su Xbox360, se è già stato confezionato per un&#39;altra piattaforma Primetime, come iOS, Android o Desktop.

Un&#39;avvertenza con Xbox360 è che deve sempre raggiungere un server chiave ogni volta che si incontra un tag EXT-X-KEY in M3U8. A differenza di iOS, dove un&#39;impostazione di Criteri DRM (policy.requireKeyServer) fa sì che il lettore video di iOS Primetime recuperi la chiave di decrittografia AES da localhost, Xbox tenterà sempre di recuperare la chiave di decrittografia da un keyserver remoto. Non esiste alcun diritto per i criteri DRM per istruire l&#39;app Xbox a recuperare la chiave di decrittografia AES da localhost. A causa di questo requisito, le voci EXT-X-KEY devono trovarsi nell’elemento M3U8 che punta all’endpoint DRM di Primetime Cloud. Questo URL è impostato tramite &lt;key_url> nel file di configurazione offlinePackager.jar config_hls.xml.

Se si desidera creare un pacchetto del contenuto una volta e inviarlo in streaming a tutte le destinazioni Primetime e configurare i dispositivi iOS in modo che non recuperino una chiave da un keyserver remoto, è possibile creare un pacchetto del contenuto utilizzando un criterio DRM con proprietà policy.requireKeyServer=false (ad esempio in policy_ios_localkeyserver.pol). I dispositivi iOS recupereranno la chiave AES localmente, mentre i dispositivi Xbox ignoreranno questa proprietà e si rivolgeranno al server della chiave DRM di Primetime Cloud per una chiave di decrittografia.

>!Nota
>
>Tutte le richieste di Xbox360 devono utilizzare l&#39;autenticazione personalizzata/>l&#39;adesione.Ciò è dovuto al fatto che sulla piattaforma Xbox360 Xbox Live >utilizza un token XSTS (Secure Token Server) di Xbox per scopi di autenticazione.
>Il server di licenze Primetime Cloud DRM utilizza il token XSTS per convalidare l’integrità sia del dispositivo Xbox che dell’utente che effettua la richiesta di licenza. Tuttavia, la convalida del token XSTS richiede la chiave del fornitore Xbox Live privato di un cliente, che Primetime Cloud DRM >non memorizza. Per questo motivo, quando Primetime Cloud DRM riceve una richiesta di licenza da un client Xbox 360, Primetime Cloud DRM inoltra il token XSTS al server Back-End >Authentication/Entitlement del cliente Primetime. Il server del cliente Primetime
>analizza e convalida quindi il token XSTS per assicurarsi che sia stato firmato utilizzando la chiave di pubblicazione dell’applicazione del cliente.
>Per passare un token XSTS dal client Xbox360, imposta il token in modo sincrono in risposta all’evento MediaPlayer.RequestKeyAttribute >descritto più dettagliatamente qui: **Imposta il token XSTS nel lettore.** Un esempio di server Back-End Authentication/Entitlement è incluso con la versione del software nella directory Custom Authentication e Entitlement.La convalida dei token XSTS è discussa in maggior dettaglio qui: **Convalida del token XSTS di Xbox Live.**


## Imposta il token XSTS nel lettore {#set-the-xsts-token-in-your-player}

In Xbox360, il token viene impostato in modo asincrono in risposta al `MediaPlayer.RequestKeyAttribute` evento.

Imposta il token XSTS.

L’app di esempio fornita con il software mostra come impostare il token XSTS nel lettore. Di seguito è riportato lo snippet di codice relativo dal sample player:

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

## Convalida del token Xbox Live XSTS {#xbox-live-xsts-token-validation}

Per le richieste XSTS, il `customerSpecificAuthToken` contiene il token XSTS con codifica Base64. Il campione `XSTSValidator` Il codice esamina il token decodificato Base64 per verificare l&#39;esistenza `EncryptedAssertion` ; tuttavia, puoi utilizzare altri metodi per distinguere tra queste richieste e quelle non Xbox. Ad esempio, puoi utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta sovrascriverà il criterio originale nei metadati DRM forniti con la richiesta della chiave Xbox. Il client Xbox supporta solo un sottoinsieme di funzioni della policy, e questi campi sono gli unici che sovrascriveranno la policy originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decrittografia e la convalida dei token. È necessario caricare [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] credenziali in un keystore in formato JKS, che fornisci al server di adesione back-end come proprietà di sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l’alias `xsts`, e il certificato di convalida del token ha l’alias `xsts-verify-cert`. È inoltre possibile eseguire l&#39;override di queste proprietà utilizzando le proprietà di sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` non ha un valore predefinito e contiene la password del keystore. Le proprietà di sistema lette da `XSTSValidator` di seguito sono riepilogati i codici:

| Proprietà di sistema | Valore predefinito | Commento |
|---|---|---|
| xsts-keystore | xsts.jks | keystore in formato JKS utilizzato dalla convalida. |
| xsts-keystore-password | | Password per il keystore |
| xsts-alias | xsts | Alias utilizzato per recuperare la chiave di decrittografia dal keystore |
| xsts-verify-cert-alias | xsts-verify-cert | Alias utilizzato per recuperare il certificato di convalida dal keystore |

## Creare JKS per una convalida XSTS{#create-jks-for-an-xsts-validator}

1. Individua il nome alias del certificato privato, che si trova nel partner [!DNL .pfx] file.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Converti [!DNL .pfx] a [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (dove `<alias>` è il nome alias del certificato privato individuato nel passaggio 1.)
1. Importa [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Inserisci [!DNL xsts.jks] nella home directory Tomcat e definire `-Dxsts-keystore-password=****` per Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] utilizzano password diverse, aggiorna il `xsts` password in `jks` per farle uguali.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
