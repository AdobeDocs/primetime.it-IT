---
title: Convalida del token Xbox Live XSTS
description: Convalida del token Xbox Live XSTS
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Convalida del token Xbox Live XSTS{#xbox-live-xsts-token-validation}

Per le richieste XSTS, il `customerSpecificAuthToken` contiene il token XSTS con codifica Base64. Il campione `XSTSValidator` Il codice esamina il token decodificato Base64 per verificare l&#39;esistenza `EncryptedAssertion` ; tuttavia, puoi utilizzare altri metodi per distinguere tra queste richieste e quelle non Xbox. Ad esempio, puoi utilizzare un URL diverso.

Il criterio restituito nel messaggio di risposta sovrascriverà il criterio originale nei metadati DRM forniti con la richiesta della chiave Xbox. Il client Xbox supporta solo un sottoinsieme di funzioni della policy, e questi campi sono gli unici che sovrascriveranno la policy originale.

Sono necessari ulteriori passaggi di configurazione per supportare la decrittografia e la convalida dei token. È necessario caricare [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] credenziali in un keystore in formato JKS, che fornisci al server di adesione back-end come proprietà di sistema `xsts-keystore`. Per impostazione predefinita, il partner [!DNL .pfx] ha l’alias `xsts`, e il certificato di convalida del token ha l’alias `xsts-verify-cert`. È inoltre possibile eseguire l&#39;override di queste proprietà utilizzando le proprietà di sistema. Infine, esiste una proprietà di sistema `xsts-keystore-password` non ha un valore predefinito e contiene la password del keystore. Le proprietà di sistema lette da `XSTSValidator` di seguito sono riepilogati i codici:

| Proprietà di sistema | Valore predefinito | Commento |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | keystore in formato JKS utilizzato dalla convalida. |
| `xsts-keystore-password` |  | Password per il keystore |
| `xsts-alias` | `xsts` | Alias utilizzato per recuperare la chiave di decrittografia dal keystore |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizzato per recuperare il certificato di convalida dal keystore |

