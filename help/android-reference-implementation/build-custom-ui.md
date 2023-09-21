---
description: Puoi creare facilmente un’interfaccia utente personalizzata basata sul framework di implementazione di riferimento.
title: Creare un’interfaccia utente personalizzata
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Creare un’interfaccia utente personalizzata {#build-a-custom-user-interface}

Puoi creare un’interfaccia utente personalizzata basata sul framework di implementazione di riferimento.

I componenti dell’interfaccia utente delle seguenti funzioni sono già integrati:

* Annunci cliccabili
* Sovrapposizioni annuncio
* Audio di associazione tardiva
* Sottotitoli
* Listener per tutti i componenti di cui sopra

1. Modifica il [!DNL PlayerFragment.java] per inizializzare i componenti dell’interfaccia utente che desideri utilizzare nel lettore.

1. Modifica il [!DNL res/player/player_fragment.xml] per personalizzare l&#39;interfaccia utente.
1. Crea il progetto.

>[!NOTE]
>
>Per apportare modifiche all&#39;interfaccia utente della barra di ricerca, è possibile modificare la classe MarkableSeekBar. Il [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) la classe gestisce il cursore, il pollice del cursore, il portaparole, gli indicatori di cue, l&#39;intervallo di buffer e gli sfondi dell&#39;intervallo di ricerca.
