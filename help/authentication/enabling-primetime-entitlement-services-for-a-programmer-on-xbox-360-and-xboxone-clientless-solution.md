---
title: Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e XboxOne Clientless
description: Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e XboxOne Clientless
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e XboxOne Clientless {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.




1. Il programmatore crea un ticket Zendesk per abilitare la soluzione Xbox 360/One per l&#39;autenticazione client di Primetime fornendo le seguenti informazioni:

   1. Piattaforma: Ad esempio Xbox 360, Xbox One

   1. ID richiedente: ad esempio netgeo, CNN, ecc.

1. Adobe creerà i certificati X509 e configurerà la chiave privata e la password alla sua fine.

1. L&#39;Adobe fornirà il certificato pubblico (di X509 cert) al programmatore nel ticket o via e-mail.

1. Il programmatore dovrebbe quindi installare tale certificato pubblico sul portale GDNP per l&#39;app registrata in Microsoft.

1. Il programmatore richiederà il JWT (Java Web Token) o il Token STS per XboxOne o 360 rispettivamente dal servizio Microsoft Xbox Live, che verrebbe crittografato utilizzando il certificato pubblico X509 fornito al passaggio 3.

1. Questi sono i token che contengono l&#39;ID dispositivo univoco per i dispositivi Xbox. Includi il token (JWT o STS) nell’intestazione Autorizzazione utilizzando un parametro &#39;x&#39; come segue:

   1. Per Xbox 360, il token XSTS deve essere codificato in Base64 prima di inviare l&#39;autenticazione a pagamento Primetime.
   1. Per Xbox One, il JWT è già codificato correttamente, quindi non dovrebbe verificarsi alcuna codifica aggiuntiva. 

1. Tutte le chiamate API dal dispositivo Xbox devono contenere l&#39;intestazione di autorizzazione con il token menzionato sopra nel parametro x.

 

>[!NOTE]
>
>In particolare, la Xbox ha alcuni requisiti unici relativi alla firma digitale. L’ID dispositivo della console XBox è incluso nel token XSTS.  Per Xbox 360, si tratta di un&#39;asserzione SAML crittografata; per Xbox One, questo è un JWT crittografato. L’app console XBox invia l’intero token XSTS all’autenticazione a pagamento di Primetime. Primetime pay-TV authentication decrittografa il token utilizzando la sua chiave pubblica, analizza il token ed estrae il deviceId da esso.

>[!NOTE]
>
>A causa della grande lunghezza del token XSTS, la console XBox ha una limitazione tecnica: non può inviare il token come server HTTP alle API di autenticazione a pagamento Primetime. Per risolvere questo problema, Primetime pay-TV authentication consente di inviare il token XSTS come parte dell’intestazione HTTP &quot;Authorization&quot; quando si chiamano le API. Il token XSTS deve essere crittografato utilizzando la chiave pubblica dal certificato X.509 rilasciato al programmatore dall&#39;autenticazione a pagamento di Primetime. Primetime pay-TV authentication memorizza la chiave privata associata e la utilizza per decrittografare il token XSTS ed estrarre il deviceId da essa.  


