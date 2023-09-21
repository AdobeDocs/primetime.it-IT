---
description: Esistono alcuni modi per determinare l’inserimento e il posizionamento degli annunci.
title: Inserimento e posizionamento di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Inserimento e posizionamento di annunci{#ad-insertion-and-placement}

Esistono alcuni modi per determinare l’inserimento e il posizionamento degli annunci.

## Inserimento di annunci {#section_1F7581B987704E318E064082190E8243}

Ecco una panoramica del processo utilizzato per determinare l’inserimento di annunci:

1. **Rilevamento opportunità**: TVSDK utilizza le informazioni di flusso per rilevare posizioni possibili e desiderate per gli annunci.
1. **Risoluzione annuncio**: TVSDK comunica con un server di annunci per recuperare gli annunci da inserire nel contenuto.
1. **Posizionamento degli annunci**: TVSDK carica gli annunci specificati e li inserisce nelle interruzioni pubblicitarie nella timeline del contenuto nelle posizioni specificate e, se necessario, ricalcola la timeline virtuale.

## Posizionamento degli annunci {#section_B9D63F7409A2447F9FF209289BE5D3D5}

Il TVSDK può ottenere le posizioni per un possibile posizionamento degli annunci dalle seguenti sorgenti:

* **Metadati/riferimenti manifesto**

  Il TVSDK rileva i segnali, estrae le informazioni necessarie da questi segnali e comunica con un server pubblicitario per ottenere gli annunci corrispondenti. Questa sorgente è comune per i flussi live/lineari.

  Il TVSDK di solito sostituisce il contenuto principale con gli annunci nella posizione indicata dai metadati o dai segnali; altrimenti, il client si ritroverebbe sempre più indietro rispetto al punto di attivazione effettivo.

* **Mappa del server pubblicitario**

  Di solito, i metadati relativi a questi flussi vengono registrati nel server pubblicitario prima della riproduzione. TVSDK recupera la timeline dell’annuncio e gli annunci corrispondenti dal server. Questa origine è comune per i flussi VOD.

  Il TVSDK di solito inserisce gli annunci risolti nel contenuto principale come indicato dalla mappa del server.

>[!NOTE]
>
>Per impostazione predefinita, TVSDK utilizza segnali manifesti per flussi live/lineari e mappe server pubblicitarie per flussi VOD. Tuttavia, per supportare la riproduzione completa degli eventi live, l’applicazione deve effettuare ulteriori operazioni.
