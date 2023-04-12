---
title: SSO tramite autenticazione passiva
description: SSO tramite autenticazione passiva
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# SSO tramite autenticazione passiva

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Introduzione

Scopo del presente documento è descrivere l&#39;implementazione del flusso di autenticazione passiva e come questo funziona con il nostro approccio standard single sign-on.

## Usecs

L&#39;autenticazione Adobe Primetime abilita il Single Sign-On (SSO) tra app/siti. Dopo che un utente effettua l’accesso con le proprie credenziali MVPD, Adobe Primetime Authentication genera un token sicuro che rappresenta la sessione di autenticazione dell’MVPD e lo associa al dispositivo dell’utente utilizzando un ID dispositivo. L’autenticazione Adobe Primetime memorizza il token o l’ID dispositivo su un server o sul dispositivo.

Finché il token è ancora valido, gli utenti appariranno direttamente come autenticati. Ciò consente agli utenti di immettere le proprie credenziali meno frequentemente mantenendo le transazioni sicure.



Il caso d&#39;uso aziendale descritto qui è un requisito molto specifico: che l&#39;utente DEVE essere autenticato almeno una volta per ogni sito visitato. Questo consente all&#39;MVPD di applicare le regole aziendali associate alla sessione authN che possono variare a seconda della rete. È in conflitto con la promessa TVE corrente che un utente deve effettuare l’accesso una sola volta e sarà autenticato su tutti i siti che fanno parte dell’ecosistema di autenticazione di Adobe Primetime.



Per mantenere la regola business ma anche mantenere una buona esperienza utente, l&#39;MVPD NON richiede che un utente fornisca manualmente le informazioni sulle credenziali. Possiamo beneficiare del cookie di sessione precedentemente impostato e tentare di eseguire una nuova autenticazione automatica utilizzando il flusso passivo; dal punto di vista dell&#39;utente, apparirà come connesso automaticamente.



Per risolvere questi problemi, abbiamo implementato 2 caratteristiche distinte: autenticazione per rete e supporto di autenticazione passiva. Gli MVPD supporteranno SAML passive authN dove stanno semplicemente riautenticando un utente se esiste una sessione authN sull&#39;IdP, indipendentemente dal sito in cui è stata creata la sessione.



## Autenticazione per rete

Questa funzione assicura che l&#39;MVPD riceva una richiesta di autenticazione una volta per ogni sito visitato. Questa funzionalità significa che un token di autenticazione di Adobe Primetime sarà associato al requestorID, quindi valido solo per la rete che lo ha richiesto. Di conseguenza, una volta che l&#39;utente si autentica sul sito &quot;A&quot; e successivamente visita il sito &quot;B&quot;, sarà necessario eseguire l&#39;autenticazione.



Si noti che, a causa del fatto che sull&#39;MVPD IdP l&#39;utente è già autenticato, non sarà richiesto di fornire le informazioni di accesso, ma invece il browser verrà semplicemente reindirizzato dal sito &quot;B&quot; all&#39;MVPD IdP e poi di nuovo. Lo stesso utente sarà ancora autenticato sul sito &quot;A&quot; se ritorna.



Il flusso seguente rappresenta la funzione di base Autenticazione per rete:





## Autenticazione passiva

L&#39;obiettivo è quello di rendere il processo di riautenticazione in background senza la necessità di un reindirizzamento completo del browser e la visualizzazione del selettore. Di conseguenza, un utente che si sposta dal sito A al sito B sarà automaticamente autenticato.



Da una prospettiva UX non ci sarà alcuna differenza tra questo flusso e un flusso eseguito con un MVPD regolare. Ciò che l&#39;utente vede è che dopo aver inserito le credenziali come risultato della visita al sito A, verrà autenticato automaticamente sul sito B.



Per rendere questo flusso fattibile, l&#39;MVPD dovrà supportare l&#39;autenticazione passiva in modo che l&#39;iframe nascosto non sia &quot;bloccato&quot; sulla pagina di accesso nel caso in cui l&#39;MVPD non abbia più una sessione. Questo viene fatto tramite l’attributo standard &quot;isPassive&quot;.



Il diagramma seguente illustra il flusso migliorato e l’autenticazione passiva &quot;dietro le quinte&quot;:





Esempio di richiesta SAML Ecco un esempio di richiesta SAML per il flusso passivo di authN:


```xml
<saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
                     AssertionConsumerServiceURL="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                     Destination="https://mvpd_idp_url"
                     ForceAuthn="false"
                     ID="_15056686-399c-4528-b21a-4a9542cfc8ec"
                     IsPassive="true"
                     IssueInstant="2014-11-03T14:18:12.394Z"
                     ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                     Version="2.0"
                     >
    <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth.adobe.com </saml2:Issuer>
    <saml2p:Extensions>
        <thrpty:RespondTo xmlns:thrpty="urn:oasis:names:tc:SAML:protocol:ext:third-party">https://saml.sp.auth.adobe.com</thrpty:RespondTo>
    </saml2p:Extensions>
    <saml2p:NameIDPolicy AllowCreate="true"
                         Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
                         SPNameQualifier="https://saml.sp.auth.adobe.com"
                         />
</saml2p:AuthnRequest>
```

Gli MVPD delle regole aziendali hanno restrizioni specifiche dell&#39;ambito SSO del dominio. Ad esempio, solo alcuni domini potrebbero essere consentiti da alcuni MVPD (SSO per la stessa società di media ma non tra società).
Alcuni MVPD potrebbero richiedere l&#39;applicazione di regole di autenticazione diverse. Ad esempio, gli MVPD potrebbero avere TTL di autenticazione diversi per reti diverse. Inoltre, gli MVPD possono abilitare l&#39;autenticazione basata su casa per alcune reti ma non per altre (i casi di utilizzo di controllo genitori sono fortemente rappresentati qui).


Questi requisiti aziendali devono tenere presente che il caso d’uso principale è che l’utente non deve essere obbligato ad accedere di nuovo dopo aver effettuato l’accesso con il proprio MVPD.

Questo può essere ottenuto utilizzando l’autenticazione per rete con flag passivo authN.



Limitazioni note iOS - A causa della natura dell&#39;archiviazione locale iOS, i flussi SSO non funzionano su iOS per le applicazioni sviluppate da diversi fornitori. Per ulteriori informazioni sull&#39;SSO in iOS 8 e versioni successive, consulta questa nota tecnica.


<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Primetime authentication Access Enabler
-->