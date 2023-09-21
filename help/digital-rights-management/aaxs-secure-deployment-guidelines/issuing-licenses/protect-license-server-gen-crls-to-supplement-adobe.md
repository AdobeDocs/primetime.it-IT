---
title: Genera CRL per integrare quelli pubblicati da Adobe
description: Genera CRL per integrare quelli pubblicati da Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Genera CRL per integrare quelli pubblicati da Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access consente di creare CRL per integrare il CRL del computer pubblicato da Adobe. L’SDK di Adobe Access controlla e applica i CRL di Adobe. Tuttavia, è possibile non consentire l’utilizzo di computer client aggiuntivi creando un CRL che revochi credenziali computer aggiuntive. A questo scopo, devi passare il CRL all’SDK di accesso per utenti Adobi, quindi, quando rilasci una licenza, l’SDK controlla sia il CRL di Adobe che il tuo.

Per ulteriori informazioni sulla generazione di CRL, consulta `RevocationListFactory` in *Riferimento API per l’accesso agli Adobi*.
