---
seo-title: Concatenamento delle licenze migliorato
title: Concatenamento delle licenze migliorato
uuid: 5e4e825a-de84-4ab2-a652-02cc03153957
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Concatenamento delle licenze migliorato {#enhanced-license-chaining}

È possibile utilizzare il concatenamento avanzato delle licenze per aggiornare una licenza utilizzando una licenza principale padre per l&#39;aggiornamento batch delle licenze.

Primetime DRM 2.0 supporta la concatenazione delle licenze in cui sia le licenze foglia che le licenze radice sono associate a un computer specifico. Primetime DRM 3.0 e versioni successive supporta la concatenazione di licenze avanzata, in cui una foglia è associata a una licenza radice, e solo la licenza principale è associata a un computer o a un dominio specifico. Il concatenamento avanzato delle licenze supporta l&#39;incorporazione di una licenza foglia con il contenuto, e il client deve solo acquisire la licenza radice dal server licenze per utilizzare il contenuto protetto.

Se si desidera abilitare il concatenamento avanzato delle licenze, è necessario assegnare una chiave di crittografia principale a un criterio DRM di Primetime. La chiave di crittografia principale viene utilizzata per eseguire un binding crittografato della licenza foglia con la licenza radice.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Il concatenamento delle licenze migliorato è supportato dai client Primetime DRM versione 3.0 o successiva. Se un client meno recente richiede una licenza per il contenuto che supporta il concatenamento avanzato delle licenze, il server licenze può comunque rilasciare una licenza a questo client utilizzando il concatenamento delle licenze supportato da Primetime DRM 2.0.

Esempio di utilizzo: Utilizzare questa opzione per aggiornare le licenze collegate scaricando una singola licenza radice. Ad esempio, implementate modelli di iscrizione in cui è possibile riprodurre il contenuto fino a quando l&#39;utente rinnova l&#39;iscrizione su base mensile. Il vantaggio di questo approccio è che gli utenti devono solo acquistare una singola licenza per aggiornare tutte le loro licenze di abbonamento.
