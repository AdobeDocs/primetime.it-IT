---
title: Manifesto delle regole di riscrittura e recupero annunci
description: 'Manifesto delle regole di riscrittura e recupero annunci '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Regole di riscrittura e recupero annunci manifesto {#manifest-rewriting}

Primetime  Ad Insertion è in grado di riscrivere frammenti e recuperare risorse tramite semplici regole di ricerca/sostituzione.  Questo può essere utilizzato per convertire https in richieste http, che aumenterebbero le prestazioni rimuovendo handshakes TLS.  Questo può essere utilizzato anche per distribuire risorse pubblicitarie e cdn dalla stessa CDN.

Le regole sono definite come ricerca/sostituzione di espressioni regolari e possono essere utilizzate per trasformare gli URL prima dell&#39;invio, nonché dopo l&#39;inserimento in un manifesto.

Questa regola di esempio consente di convertire tutte le richieste di annunci in domain.com da https a http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

La regola seguente utilizzerà il contenuto CDN per distribuire annunci che si trovano  Adobe  CDN di archiviazione.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

Le regole possono essere denominate e abilitate/disabilitate modificando il parametro `ptprotoswitch` nell&#39;API di Bootstrap, che è un elenco separato da virgole di regole da eseguire.  Ad esempio, queste due regole possono essere eseguite impostando `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

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

Contattate il supporto tecnico per creare/abilitare queste regole per il vostro account.