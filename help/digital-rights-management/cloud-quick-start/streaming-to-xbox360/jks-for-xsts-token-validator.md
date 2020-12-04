---
seo-title: Creare JKS per una convalida XSTS
title: Creare JKS per una convalida XSTS
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Creare JKS per un validatore XSTS{#create-jks-for-an-xsts-validator}

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
