---
title: Generare CRL per integrare quelli pubblicati da Adobe
description: Generare CRL per integrare quelli pubblicati da Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Generare CRL per integrare quelli pubblicati da Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access consente di creare CRL per integrare il machine CRL pubblicato da Adobe. Adobe Access SDK controlla e applica i CRL di Adobe, tuttavia è possibile impedire l’utilizzo di computer client aggiuntivi creando un CRL che revochi le credenziali aggiuntive del computer. A questo scopo, devi passare il CRL all’SDK di Adobe Access, quindi, quando si rilascia una licenza, l’SDK controlla sia l’Adobe CRL che il tuo CRL.

Per ulteriori informazioni sulla generazione dei CRL, consulta `RevocationListFactory` in *Riferimento API di accesso agli Adobi*.
