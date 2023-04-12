---
title: Informazioni sugli ambienti Adobe
description: Informazioni sugli ambienti Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Informazioni sugli ambienti Adobe {#understanding-the-adobe-environments}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

È disponibile la documentazione ufficiale che descrive gli ambienti di Adobe [Configurazione dell’ambiente e test in Pre-equal](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Gli ambienti di Adobe, riassunti in poche parole:

Adobe dispone di due ambienti: **Pre-Qualificazione** e **Versione**.

* Nell’ambiente di pre-qualificazione stiamo preparando la nuova build da rilasciare.

* La build della versione corrente si trova nell’ambiente di rilascio.

Ogni ambiente dispone di due profili : **staging** e **produzione**.

* Il profilo di staging si connette al server di staging MVPD
* Il profilo di produzione si collega al profilo di produzione MVPD.

Il motivo per avere i due profili è che sul profilo di staging stiamo preparando nuovi partner ad andare in diretta, e loro vorrebbero testare il sistema con la prossima build (Pre-Qualification) o con il rilascio uno (più stabile).

Se un partner desidera testare la nuova versione, è necessario eseguire alcuni passaggi aggiuntivi. Vedi [Configurazione dell’ambiente e test in Pre-equal](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

Seguendo i passaggi descritti in precedenza, è sicuro che la prossima versione verrà testata nell’ambiente di pre-qualificazione.
