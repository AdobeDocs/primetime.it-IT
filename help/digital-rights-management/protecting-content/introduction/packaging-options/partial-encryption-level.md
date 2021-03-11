---
title: Livello di cifratura parziale
description: Livello di cifratura parziale
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Livello di crittografia parziale {#partial-encryption-level}

Questa opzione di packaging specifica se tutti i frame, o solo un sottoinsieme di frame, devono essere crittografati. Sono disponibili tre livelli di crittografia: bassa, media e alta.

>[!NOTE]
>
>La crittografia parziale si applica solo alla traccia video in file F4V/MP4.

La cifratura parziale è progettata per dare ai fornitori di contenuti granularità necessaria per codificare il contenuto in parti. La crittografia del contenuto aggiunge il sovraccarico della CPU al dispositivo che sta decrittografando e visualizzando il contenuto. Utilizza la crittografia parziale per ridurre il sovraccarico della CPU mantenendo al tempo stesso una protezione molto elevata del contenuto. L’utilizzo di questa funzione è motivato da un singolo contenuto destinato a essere riprodotto su dispositivi a basso, medio e alto consumo energetico.

A causa della natura della codifica video, non è necessario crittografare il 100% del video per renderlo non riproducibile in caso di furto. La cifratura parziale dispone di tre impostazioni: bassa, media e alta; le percentuali di cifratura associate dipendono dalla modalità di codifica del video. A causa di questa dipendenza di codifica, la percentuale di contenuto crittografato rientra nei seguenti intervalli:

* Alta: Cifra tutti i campioni.
* Media: Cifra una destinazione pari al 50% dei dati.
* Bassa: Cifra una destinazione dal 20 al 30% dei dati.

Queste impostazioni sono state progettate utilizzando la seguente regola: Anche qualsiasi contenuto crittografato con l’impostazione bassa viene crittografato con l’impostazione media. In tal modo, lo stesso contenuto distribuito a bassa crittografia da una parte e distribuito a crittografia media da un’altra parte non compromette la protezione del contenuto.

Esempio di utilizzo: La riduzione del livello di crittografia riduce il sovraccarico della decrittografia sul client e migliora le prestazioni di riproduzione su computer di fascia bassa.
