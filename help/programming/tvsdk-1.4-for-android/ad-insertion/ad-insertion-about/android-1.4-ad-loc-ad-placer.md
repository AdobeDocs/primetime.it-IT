---
description: Esistono alcuni modi per determinare l’inserimento degli annunci e il posizionamento degli annunci.
title: Inserimento e posizionamento di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Inserimento e posizionamento di annunci{#ad-insertion-and-placement}

Esistono alcuni modi per determinare l’inserimento degli annunci e il posizionamento degli annunci.

## Inserimento annuncio {#section_1F7581B987704E318E064082190E8243}

Ecco una panoramica del processo utilizzato per determinare l&#39;inserimento di annunci:

1. **Rilevamento** opportunità: Il TVSDK utilizza le informazioni di flusso per rilevare le posizioni possibili e desiderate per gli annunci.
1. **Risoluzione** annunci: Il TVSDK comunica con un server di annunci per recuperare gli annunci da unire nel contenuto.
1. **Posizionamento** dell’annuncio: Il TVSDK carica gli annunci specificati e li inserisce nella timeline del contenuto nelle posizioni specificate e, se necessario, ricalcola la timeline virtuale.

## Posizionamento annuncio {#section_B9D63F7409A2447F9FF209289BE5D3D5}

Il TVSDK può ottenere le posizioni per un possibile posizionamento di annunci dalle seguenti sorgenti:

* **Metadati/suggerimenti manifesto**

   Il TVSDK rileva i suggerimenti, estrae le informazioni necessarie da questi suggerimenti e comunica con un server pubblicitario per ottenere gli annunci corrispondenti. Questa sorgente è comune per i flussi live/lineari.

   Il TVSDK di solito sostituisce il contenuto principale con gli annunci nella posizione indicata dai metadati/suggerimenti; in caso contrario, il cliente scenderebbe sempre di più dietro l&#39;effettivo live point.

* **Mappa del server pubblicitario**

   Di solito, i metadati relativi a questi flussi vengono registrati nel server pubblicitario prima della riproduzione. Il TVSDK recupera la timeline dell’annuncio e gli annunci corrispondenti dal server. Questa fonte è comune per i flussi VOD.

   TVSDK di solito inserisce gli annunci risolti nel contenuto principale come indicato dalla mappa del server.

>[!NOTE]
>
>Per impostazione predefinita, il TVSDK utilizza segnali manifest per flussi live/lineari e mappe del server pubblicitario per flussi VOD. Tuttavia, per supportare la riproduzione completa degli eventi per gli eventi live, l’applicazione deve intraprendere ulteriori passi.

