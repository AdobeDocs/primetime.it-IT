---
title: Livello di crittografia parziale
description: Livello di crittografia parziale
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Livello di crittografia parziale {#partial-encryption-level}

Questa opzione di creazione pacchetti specifica se tutti i fotogrammi o solo un sottoinsieme di fotogrammi devono essere crittografati. Sono disponibili tre livelli di crittografia: basso, medio e alto.

>[!NOTE]
>
>La crittografia parziale si applica solo alla traccia video nei file F4V/MP4.

La crittografia parziale è progettata per fornire ai provider di contenuti granularità per codificare il contenuto in parti. La crittografia del contenuto aggiunge un sovraccarico della CPU al dispositivo che decrittografa e visualizza il contenuto. Utilizzare la crittografia parziale per ridurre il sovraccarico della CPU mantenendo al contempo una protezione molto elevata del contenuto. Una motivazione per l&#39;utilizzo di questa funzione è un singolo contenuto destinato ad essere riproducibile su dispositivi a bassa, media e alta potenza.

A causa della natura della codifica video, non è necessario crittografare il 100% del video per renderlo non riproducibile in caso di furto. La cifratura parziale dispone di tre impostazioni, bassa, media e alta, e le percentuali di cifratura associate dipendono da come il video è codificato. A causa di questa dipendenza di codifica, la percentuale di contenuto crittografato rientra nei seguenti intervalli:

* Alta: crittografa tutti i campioni.
* Medio: crittografa il 50% dei dati di destinazione.
* Bassa: crittografa una destinazione dal 20 al 30% dei dati.

Queste impostazioni sono state progettate utilizzando la seguente regola: Anche qualsiasi contenuto crittografato con l’impostazione bassa viene crittografato con l’impostazione media. In questo modo, lo stesso contenuto distribuito a bassa crittografia da una parte e distribuito a media crittografia da un&#39;altra parte non compromette la protezione del contenuto.

Caso d’uso di esempio: la riduzione del livello di crittografia riduce il sovraccarico di decrittografia sul client e migliora le prestazioni di riproduzione sui computer di fascia bassa.
