---
title: Consenti MVPD nella finestra di dialogo di selezione
description: Consenti MVPD nella finestra di dialogo di selezione
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Consenti MVPD nella finestra di dialogo di selezione {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Problema {#issue}

Il programmatore potrebbe voler testare o controllare l&#39;esperienza utente delle nuove integrazioni MVPD prima di passare al pubblico per gli utenti finali.

## Soluzione {#solution}

In `displayProviderDialog()` callback, l&#39;autenticazione Adobe Primetime restituisce tutti gli MVPD integrati con il programmatore selezionato (Requestor ID). Ma il programmatore può applicare un filtro sull&#39;array di ritorno degli MVPD e visualizzare solo quelli che si trovano in entrambi gli elenchi.

## Esempio {#example}

Questo esempio illustra come visualizzare solo CableCompany_1 e CableCompany_2 all&#39;interno della finestra di dialogo del selettore MVPD e come non mostrare CableCompany_NewIntegration.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if ( isAllowListed(currentMvpd.ID) ) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isAllowListed(mvpdID) {
    // Implement allowlisting on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
}
```

<!--
**Related Information**
* [Prevent MVPDs from appearing in the Selection Dialog](/help/authentication/prevent-mvpd-selectn-dialog.md)
* **Code Samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->