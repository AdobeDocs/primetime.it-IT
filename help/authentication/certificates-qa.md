---
title: Domande e risposte sui certificati
description: Domande e risposte sui certificati
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---



# Domande e risposte sui certificati {#certificates-q}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

**Q1:** È possibile registrare i certificati in iOS e Android?

**R:** Il certificato per iOS e Android è lo stesso nella configurazione corrente. Il certificato nativo viene utilizzato per entrambe le piattaforme.

</br>

**Q2:** Gli stessi certificati iOS possono essere utilizzati come certificati di primario e backup negli ambienti di produzione e staging? Se non è consigliato, è possibile fornire una spiegazione?

**R:** Non ha senso configurare lo stesso certificato sia del certificato primario che del certificato di backup. Abbiamo il concetto di certificati di primario e di backup in modo da poter configurare più certificati per un programmatore in caso di scadenza o revoca del certificato primario. Avere un certificato di backup darà ai programmatori il tempo di cambiare quello primario senza influire sull&#39;ambiente di rilascio. È tuttavia possibile utilizzare lo stesso set di certificati Primari e Backup per i profili Produzione e Staging.

</br>

**Q3:** È necessario un nuovo certificato per le pagine web che utilizzeranno il nuovo TempPass flessibile? 

**R:** Il certificato (e qualsiasi certificato) è configurato a livello di Media Company &amp; Programmer. FlexibleTempPass è un MVPD, non è necessario configurare alcun certificato per esso, quindi se si sta integrando un programmatore esistente con TempPass flessibile, verrà utilizzato il certificato già configurato a livello di Programmer / Media Company.

