---
title: Convalida token XSTS per Xbox Live
description: Convalida token XSTS per Xbox Live
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Convalida token XSTS Xbox Live{#xbox-live-xsts-token-validation}

Per le richieste XSTS, il campo `customerSpecificAuthToken` conterrà il token XSTS codificato Base64. Il codice di esempio `XSTSValidator` esamina il token decodificato Base64 per verificare l&#39;esistenza dell&#39;elemento `EncryptedAssertion`; tuttavia, puoi utilizzare altri metodi per distinguere tra queste richieste e richieste non Xbox. Ad esempio, puoi utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta ignorerà il criterio originale nei metadati DRM forniti con la richiesta di chiave Xbox. Solo un sottoinsieme di funzionalità dei criteri è supportato dal client Xbox e questi campi sono gli unici che ignoreranno il criterio originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decrittografia e la convalida dei token. È necessario caricare le credenziali [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] in un archivio chiavi in formato JKS, che viene quindi fornito al server di adesione back-end come proprietà del sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l’alias `xsts` e il certificato di convalida del token ha l’alias `xsts-verify-cert`. È inoltre possibile ignorarli utilizzando le proprietà del sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` che non ha un valore predefinito e che contiene la password del keystore. Le proprietà di sistema lette dal codice `XSTSValidator` sono riepilogate di seguito:

| Proprietà di sistema | Valore predefinito | Commento |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Archivio chiavi in formato JKS utilizzato dalla convalida. |
| `xsts-keystore-password` |  | Password per il keystore |
| `xsts-alias` | `xsts` | Alias utilizzato per recuperare la chiave di decrittografia dal keystore |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizzato per recuperare il certificato di convalida dal keystore |

