---
seo-title: Convalida token Xbox Live XSTS
title: Convalida token Xbox Live XSTS
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Convalida token Xbox Live XSTS{#xbox-live-xsts-token-validation}

Per le richieste XSTS, il campo `customerSpecificAuthToken` conterrà il token XSTS codificato Base64. Il codice di esempio `XSTSValidator` esamina il token decodificato Base64 per verificare l&#39;esistenza dell&#39;elemento `EncryptedAssertion`; tuttavia, potete utilizzare altri metodi per distinguere tra queste richieste e richieste non Xbox. Ad esempio, potete utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta ignorerà il criterio originale nei metadati DRM forniti con la richiesta della chiave Xbox. Solo un sottoinsieme delle funzionalità del criterio è supportato dal client Xbox e questi campi sono gli unici che ignoreranno il criterio originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decodifica e la convalida dei token. È necessario caricare le credenziali [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] in un archivio di chiavi in formato JKS, che vengono quindi fornite al server di adesione back-end come proprietà di sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l&#39;alias `xsts` e il certificato di convalida del token ha l&#39;alias `xsts-verify-cert`. È inoltre possibile ignorare tali impostazioni utilizzando le proprietà di sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` che non ha valore predefinito e che contiene la password dell&#39;archivio di chiavi. Le proprietà di sistema lette dal codice `XSTSValidator` sono riepilogate di seguito:

| Proprietà del sistema | Valore predefinito | Commento |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Keystore di formato JKS utilizzato dal validatore. |
| `xsts-keystore-password` |  | Password per l&#39;archivio chiavi |
| `xsts-alias` | `xsts` | Alias utilizzato per recuperare il tasto di decrittazione dall&#39;archivio di chiavi |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizzato per recuperare il certificato di convalida dall&#39;archivio chiavi |

