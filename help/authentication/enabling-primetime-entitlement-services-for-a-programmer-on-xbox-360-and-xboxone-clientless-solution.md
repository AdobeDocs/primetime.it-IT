---
title: Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e Xbox One Clientless
description: Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e Xbox One Clientless
exl-id: ff7254de-9ea4-4c27-a186-d1c2eea12222
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e Xbox One Clientless {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.




1. Il programmatore crea un ticket Zendesk per abilitare Xbox 360/One per la soluzione client di autenticazione Primetime fornendo le seguenti informazioni:

   1. Piattaforma: ad esempio Xbox 360, Xbox One

   1. ID richiedente: ad esempio netgeo, CNN, ecc.

1. Adobe creerà certificati X509 e configurerà la chiave privata e la password alla fine.

1. L’Adobe fornirà il certificato pubblico (di certificato X509) al programmatore nel ticket o tramite e-mail.

1. Il programmatore dovrebbe quindi installare tale certificato pubblico sul portale GDNP per l’app registrata in Microsoft.

1. Il programmatore richiederà quindi il token JWT (Java Web Token) o STS per XboxOne o 360 rispettivamente dal servizio Microsoft Xbox Live, che verrebbe crittografato utilizzando il certificato pubblico X509 fornito al passaggio 3.

1. Questi sono i token che contengono l&#39;ID dispositivo univoco per i dispositivi Xbox. Includi il token (JWT o STS) nell’intestazione Autorizzazione utilizzando un parametro &quot;x&quot; come segue:

   1. Per Xbox 360, il token XSTS deve essere codificato in Base64 prima di essere inviato all’autenticazione della pay-TV Primetime.
   1. Per Xbox One, il codice JWT è già codificato correttamente, quindi non dovrebbe verificarsi alcuna codifica aggiuntiva. 

1. Tutte le chiamate API dal dispositivo Xbox devono contenere l&#39;intestazione di autorizzazione con il token indicato sopra nel parametro x.

 

>[!NOTE]
>
>La Xbox in particolare ha alcuni requisiti specifici relativi alla firma digitale. L&#39;ID dispositivo della console XBox è incluso nel token XSTS.  Per Xbox 360, si tratta di un&#39;asserzione SAML crittografata; per Xbox One, si tratta di un JWT crittografato. L’app della console XBox invia l’intero token XSTS all’autenticazione Primetime per TV a pagamento. L’autenticazione a pay-TV di Primetime decrittografa il token utilizzando la relativa chiave pubblica, lo analizza ed estrae il deviceId da esso.

>[!NOTE]
>
>A causa della lunghezza elevata del token XSTS, la console XBox ha un limite tecnico: non può inviare il token come GET HTTP alle API di autenticazione della TV a pagamento Primetime. Per risolvere questo problema, l’autenticazione della pay-TV Primetime consente di inviare il token XSTS come parte dell’intestazione HTTP &quot;Authorization&quot; quando si chiamano le API. Il token XSTS deve essere crittografato utilizzando la chiave pubblica del certificato X.509 rilasciato al programmatore dall’autenticazione della pay-TV Primetime. L’autenticazione della pay-TV di Primetime memorizza la chiave privata associata e la utilizza per decrittografare il token XSTS ed estrarre il deviceId da esso.
