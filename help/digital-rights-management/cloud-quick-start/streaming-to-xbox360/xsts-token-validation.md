---
seo-title: Convalida token Xbox Live XSTS
title: Convalida token Xbox Live XSTS
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Convalida token Xbox Live XSTS{#xbox-live-xsts-token-validation}

Per le richieste XSTS, il `customerSpecificAuthToken` campo conterrà il token XSTS codificato Base64. Il `XSTSValidator` codice di esempio esamina il token decodificato Base64 per verificare l&#39;esistenza dell&#39; `EncryptedAssertion` elemento; tuttavia, potete utilizzare altri metodi per distinguere tra queste richieste e richieste non Xbox. Ad esempio, potete utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta ignorerà il criterio originale nei metadati DRM forniti con la richiesta della chiave Xbox. Solo un sottoinsieme delle funzionalità del criterio è supportato dal client Xbox e questi campi sono gli unici che ignoreranno il criterio originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decodifica e la convalida dei token. È necessario caricare le [!DNL xsts_partner_cert.pfx] credenziali e [!DNL x_secure_token_service.part.xboxlive.com.cer] le credenziali in un archivio chiavi in formato JKS, che viene quindi fornito al server di adesione back-end come proprietà del sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l’alias `xsts`e il certificato di convalida del token ha l’alias `xsts-verify-cert`. È inoltre possibile ignorare tali impostazioni utilizzando le proprietà di sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` che non ha valore predefinito e che contiene la password dell&#39;archivio di chiavi. Le proprietà di sistema lette dal `XSTSValidator` codice sono riepilogate di seguito:

| Proprietà del sistema | Valore predefinito | Commento |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Keystore di formato JKS utilizzato dal validatore. |
| `xsts-keystore-password` |  | Password per l&#39;archivio chiavi |
| `xsts-alias` | `xsts` | Alias utilizzato per recuperare il tasto di decrittazione dall&#39;archivio di chiavi |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizzato per recuperare il certificato di convalida dall&#39;archivio chiavi |

