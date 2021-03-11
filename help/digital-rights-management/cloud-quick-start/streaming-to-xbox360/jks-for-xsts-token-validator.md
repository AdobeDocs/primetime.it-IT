---
title: Creare JKS per una convalida XSTS
description: Creare JKS per una convalida XSTS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Creare JKS per una convalida XSTS{#create-jks-for-an-xsts-validator}

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
