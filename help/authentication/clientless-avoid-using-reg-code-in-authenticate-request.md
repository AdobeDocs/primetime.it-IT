---
title: Evita di usare '&'reg_code in /authenticate Request
description: Evita di usare '&'reg_code in /authenticate Request
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Evita di usare &#39;&amp;&#39;reg_code in /authenticate Request {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>



## Problema

Il browser IE 9 interpreta &#39;\®&#39; come comando speciale e lo converte in ®. 

## Spiegazione

Se la `/authenticate` La richiesta è composta come segue...

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...verrà interpretato dal browser IE come di seguito e verrà inviato ad Adobe in questo formato:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

Il requestor\_id verrà interpretato come universale®\_code=EKAFMFI, poiché non c&#39;è &#39;&amp;&#39;, e l&#39;Adobe non troverà un `regCode` parametro con cui associare il token.  È possibile che il token AuthN non venga creato affatto, nel qual caso `/checkauthn` le chiamate non riusciranno a trovare alcun token.



## Soluzione

Una delle seguenti opzioni dovrebbe risolvere questo problema:

1. Evita di utilizzare `&reg_code` parametro tra gli altri parametri della stringa di query.  Invece spostalo sul primo parametro della stringa di query nell&#39;URL della richiesta, facendo in modo che l&#39;url della richiesta sia così:\
    

       &lt;fqdn>autentica?reg_code =EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   In questo modo, il `&reg` param non verrà interpretato in modo errato.

1. Normalizza `&reg_code` come `&amp;reg_code`.

1. Ad Adobe, se la creazione del token AuthN non è riuscita, potrebbe essere introdotta una nuova funzione per inviare nuovamente un codice di errore alla seconda schermata in risposta a una chiamata di autenticazione.

