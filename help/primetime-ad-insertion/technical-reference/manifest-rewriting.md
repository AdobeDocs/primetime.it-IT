---
title: Regole di riscrittura e recupero di annunci del manifesto
description: Regole di riscrittura e recupero di annunci del manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Regole di riscrittura e recupero di annunci del manifesto {#manifest-rewriting}

Primetime Ad Insertion è in grado di riscrivere i frammenti e recuperare le risorse utilizzando semplici regole di ricerca/sostituzione.  Può essere utilizzato per convertire https in richieste http, il che aumenterebbe le prestazioni rimuovendo gli handshake TLS.  Può essere utilizzato anche per distribuire risorse pubblicitarie e cdn dalla stessa CDN.

Le regole sono definite come ricerca/sostituzione di espressioni regolari e possono essere utilizzate per trasformare gli URL prima dell’invio o dopo l’inserimento in un manifesto.

Questa regola di esempio convertirà al ribasso tutte le richieste di annunci in domain.com da https in http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

La regola seguente utilizza la rete CDN di contenuto per distribuire gli annunci che si trovano sulla rete CDN di Adobe per l’archiviazione di annunci.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

Le regole possono essere denominate e abilitate/disabilitate modificando la `ptprotoswitch` nell’API Bootstrap, che è un elenco separato da virgole di regole da eseguire.  Ad esempio, queste due regole possono essere eseguite entrambe impostando `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

Contatta il supporto tecnico per creare/abilitare queste regole per il tuo account.
