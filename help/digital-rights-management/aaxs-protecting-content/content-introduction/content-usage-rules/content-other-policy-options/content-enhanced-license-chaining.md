---
seo-title: Concatenamento delle licenze migliorato
title: Concatenamento delle licenze migliorato
uuid: d11b0631-5dfb-42b8-b7ba-cfeb1da488be
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Concatenamento licenze migliorato {#enhanced-license-chaining}

Consente di aggiornare una licenza utilizzando una licenza principale padre per l&#39;aggiornamento batch delle licenze.

 concatenamento di licenze supportato da Access 2.0 in cui sia le licenze foglia che le licenze radice sono associate a un computer specifico.  Adobe Access 3.0 supporta la concatenazione di licenze avanzate, in cui una foglia è associata a una licenza radice, e solo la licenza principale è associata a un computer o a un dominio specifico. La concatenazione di licenze avanzata supporta l&#39;incorporazione di licenze foglia con il contenuto, e il client deve solo acquisire la licenza radice dal server licenze per utilizzare il contenuto protetto.

Per abilitare il concatenamento delle licenze avanzato, al criterio viene assegnata una chiave di crittografia radice. La chiave di crittografia principale viene utilizzata per eseguire un binding crittografato della licenza foglia con la licenza radice.

>[!NOTE]
>
>Il concatenamento avanzato delle licenze è supportato dai client di accesso al Adobe  versione 3.0 e successive. Se un client meno recente richiede una licenza per il contenuto che supporta il concatenamento avanzato delle licenze, il server licenze può comunque rilasciare una licenza a questo client utilizzando il concatenamento delle licenze supportato  Adobe Access 2.0.

Esempio di utilizzo: Utilizzare questa opzione per aggiornare le licenze collegate scaricando una singola licenza radice. Ad esempio, implementate modelli di iscrizione in cui è possibile riprodurre il contenuto fino a quando l&#39;utente rinnova l&#39;iscrizione su base mensile. Il vantaggio di questo approccio è che gli utenti devono solo effettuare una singola acquisizione di licenza per aggiornare tutte le loro licenze di abbonamento.
