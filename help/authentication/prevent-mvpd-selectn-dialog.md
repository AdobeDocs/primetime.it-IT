---
title: Impedisci la visualizzazione di MVPD nella finestra di dialogo per selezione
description: Impedisci la visualizzazione di MVPD nella finestra di dialogo per selezione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Impedisci la visualizzazione di MVPD nella finestra di dialogo per selezione

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Problema {#issue-prevent-mvpd-sel-dialog}

È necessario impedire che MVPD specifici (&quot;elenco di blocchi&quot;) vengano visualizzati nel selettore MVPD.


## Soluzione {#solution-prevent-mvpd-sel-dialog}

La soluzione consiste nell’eseguire un’inserzione di blocchi quando `displayProviderDialog()` viene chiamato.

Ad esempio, se si desidera che CableCompany_1 e CableCompany_2 non vengano visualizzati all&#39;interno del selettore MVPD, è necessario eseguire una procedura simile a quella illustrata nell&#39;esempio seguente.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->
