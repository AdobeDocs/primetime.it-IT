---
seo-title: Livello di cifratura parziale
title: Livello di cifratura parziale
uuid: dbd9ce92-c829-4cad-9ac4-c57bd4f70345
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Livello di cifratura parziale {#partial-encryption-level}

Questa opzione di package specifica se tutti i frame, o solo un sottoinsieme di frame, devono essere codificati. Sono disponibili tre livelli di crittografia: bassa, media e alta.

>[!NOTE]
>
>La cifratura parziale si applica alla traccia video solo nei file F4V/MP4.

La cifratura parziale è progettata per fornire ai fornitori di contenuto granularità necessaria per codificare il contenuto in parti. La cifratura del contenuto aggiunge il sovraccarico della CPU al dispositivo che sta decifrando e visualizzando il contenuto. Utilizzate la cifratura parziale per ridurre il sovraccarico della CPU mantenendo al contempo una protezione molto elevata del contenuto. Un caso motivante per l&#39;utilizzo di questa funzione è rappresentato da un singolo contenuto destinato a essere riprodotto su dispositivi a bassa, media e alta potenza.

A causa della natura della codifica video, non è necessario codificare il 100% del video per renderlo non riproducibile in caso di furto. La cifratura parziale ha tre impostazioni: bassa, media e alta, e le percentuali associate di cifratura dipendono dalla modalità di codifica del video. A causa di questa dipendenza di codifica, la percentuale di contenuto cifrato rientra nei seguenti intervalli:

* Alta: Cifra tutti i campioni.
* Media: Cifra una destinazione pari al 50% dei dati.
* Bassa: Cifra una destinazione dal 20 al 30% dei dati.

Queste impostazioni sono state progettate utilizzando la seguente regola: Anche il contenuto cifrato con l&#39;impostazione bassa viene cifrato con l&#39;impostazione media. In questo modo, lo stesso contenuto distribuito a bassa cifratura da una parte e distribuito a media crittografia da un&#39;altra parte non compromette la protezione del contenuto.

Esempio di utilizzo: La riduzione del livello di cifratura riduce il sovraccarico di decrittazione sul client e migliora le prestazioni di riproduzione sui computer di fascia bassa.
