---
title: Funzione di verifica preliminare, Come attivare, Risolvere i problemi o Determinare il problema
description: Funzione di verifica preliminare, Come attivare, Risolvere i problemi o Determinare il problema
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Funzione di verifica preliminare: Come attivare, risolvere i problemi o determinare il problema {#preflight-feature}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Si è verificato un cambiamento nel modo in cui l’autenticazione Adobe Primetime calcola preAuthorizeResources. L’API di pre-autorizzazione dispone di una nuova implementazione. Questa implementazione sostituisce la vecchia soluzione che prevede l’effettuazione di più chiamate di autorizzazione.
L&#39;interfaccia esterna per l&#39;API di pre-autorizzazione rimane invariata, non sono necessari aggiornamenti nell&#39;applicazione del programmatore.

Sono disponibili tre modi per calcolare le risorse di Preflight:

* **Fork e metodo di join a MVPD**: ciò comporta l&#39;Adobe di effettuare più chiamate di autorizzazione all&#39;MVPD (il cliente dovrà comunque effettuare una chiamata di verifica preliminare).
* **Line-up dei canali**: l&#39;MVPD espone la linea del canale per l&#39;utente connesso nella risposta di autenticazione SAML e l&#39;Adobe restituisce le risorse autorizzate in base a tale risposta. La risposta SAML authN nel tracciatore SAML dovrebbe esporre tale elenco.
* **Autorizzazione multicanale**: l’autenticazione client e Adobe effettua entrambe una singola chiamata all’MVPD per un set di risorse.

Indipendentemente dall’MVPD, l’applicazione client effettuerà una singola chiamata all’endpoint Preflight (API checkPreauthorizedResources), passando un set di resourceIDs. In base a uno dei metodi di cui sopra supportati da MVPD, Adobe restituirà gli ID risorsa pre-autorizzati.

Se Preflight si basa sul metodo fork &amp; join, il backend di autenticazione Adobe Primetime controlla un valore impostato per le &quot;chiamate di preautorizzazione massime&quot; nella sua configurazione. Questo è configurato da Adobe.

Il valore predefinito per la configurazione &quot;max preauthorization call&quot; è &quot;5&quot;, il che significa che al massimo 5 risorse possono essere inviate in Preflight per gli MVPD di fork e join. Se si passano più di 5 risorse, si verifica un&#39;eccezione e viene restituito un elenco nullo. Questo è il comportamento previsto. Possiamo configurarlo a qualsiasi valore se l&#39;MVPD non supporta la formazione di canali o l&#39;autorizzazione multicanale, ma solo dopo averli consultati come più chiamate di autorizzazione fork e join aumenterà i loro tempi di caricamento.

Di conseguenza, per attivare/risolvere i problemi relativi a Preflight per un MVPD, è necessario cercare questi elementi:

* Il metodo supportato dall&#39;MVPD (fork &amp; join, line-up dei canali o multi-canale).
* Se è supportato solo il fork &amp; join, è necessario chiedere al programmatore quanti ID di risorse invierà nella chiamata Preflight.
* L&#39;MVPD deve essere consultato e deve conoscere l&#39;impatto dell&#39;effettuazione di un numero &quot;n&quot; di chiamate di autorizzazione di fork &amp; join. Successivamente, il valore deve essere configurato nella configurazione se è maggiore di 5.

**Limitazione**

Nota bene che non riceviamo alcun resourceID dalla chiamata di Preflight per alcuni MVPD come AT&amp;T e TWC se uno qualsiasi degli resourceID è un falso ID o un ID non riconosciuto nell&#39;elenco degli resourceID che inviano nella chiamata di preflight anche se abbiamo risorse valide e autorizzate anche in quell&#39;elenco.

